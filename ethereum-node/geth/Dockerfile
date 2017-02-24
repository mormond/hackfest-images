FROM ethereumex/geth-dev

RUN useradd -ms /bin/bash eth-node

USER eth-node
RUN pm2 install pm2-logrotate
RUN pm2 set pm2-logrotate:max_size 100M
RUN pm2 set pm2-logrotate:compress true
RUN pm2 set pm2-logrotate:rotateInterval '23 * * *'

RUN git clone https://github.com/EthereumEx/bootnode-registrar.git /home/eth-node/lib/bootnode
WORKDIR /home/eth-node/lib/bootnode
RUN npm install

RUN git clone https://github.com/EthereumEx/eth-net-intelligence-api.git /home/eth-node/lib/ethStatsApi
WORKDIR /home/eth-node/lib/ethStatsApi
RUN npm install

RUN git clone https://github.com/mormond/NodeApp.git /home/eth-node/lib/nodeapp
WORKDIR /home/eth-node/lib/nodeapp
RUN npm install

WORKDIR /home/eth-node
ADD app.json /home/eth-node/app.json
ADD runGeth.sh /home/eth-node/runGeth.sh

ENTRYPOINT ["pm2", "start", "--no-daemon", "app.json"]


