FROM microsoft/dotnet:2.1.4-runtime-bionic

ENV DEBIAN_FRONTEND noninteractive
ENV DOTNET_CLI_TELEMETRY_OPTOUT 1

RUN apt-get update && apt-get install -y \
    unzip \
    screen \
    expect \
    libleveldb-dev \
    curl \
    libleveldb-dev \
    libssl-dev \
    vim \
    man \
    libunwind8

RUN rm -rf /var/lib/apt/lists/*

RUN latest_tag=`curl -s https://api.github.com/repos/neo-project/neo-cli/releases/latest | grep tag_name | sed -E 's/.*"([^"]+)".*/\1/'` \ 
  && curl -vLO https://github.com/neo-project/neo-cli/releases/download/$latest_tag/neo-cli-linux-x64.zip \
  && curl -vLO https://github.com/neo-project/neo-plugins/releases/download/$latest_tag/ApplicationLogs.zip \
  && curl -vLO https://github.com/neo-project/neo-plugins/releases/download/$latest_tag/CoreMetrics.zip \
  && curl -vLO https://github.com/neo-project/neo-plugins/releases/download/$latest_tag/ImportBlocks.zip \
  && curl -vLO https://github.com/neo-project/neo-plugins/releases/download/$latest_tag/RpcNep5Tracker.zip \
  && curl -vLO https://github.com/neo-project/neo-plugins/releases/download/$latest_tag/RpcSecurity.zip \
  && curl -vLO https://github.com/neo-project/neo-plugins/releases/download/$latest_tag/RpcSystemAssetTracker.zip \
  && curl -vLO https://github.com/neo-project/neo-plugins/releases/download/$latest_tag/RpcWallet.zip \
  && curl -vLO https://github.com/neo-project/neo-plugins/releases/download/$latest_tag/SimplePolicy.zip \
  && curl -vLO https://github.com/neo-project/neo-plugins/releases/download/$latest_tag/StatesDumper.zip

RUN unzip -q -d /opt/node neo-cli-linux-x64.zip && rm neo-cli-linux-x64.zip \
  && unzip -q -d /opt/node/neo-cli ApplicationLogs.zip && rm ApplicationLogs.zip \ 
  && unzip -q -d /opt/node/neo-cli CoreMetrics.zip && rm CoreMetrics.zip \ 
  && unzip -q -d /opt/node/neo-cli ImportBlocks.zip && rm ImportBlocks.zip \ 
  && unzip -q -d /opt/node/neo-cli RpcNep5Tracker.zip && rm RpcNep5Tracker.zip \ 
  && unzip -q -d /opt/node/neo-cli RpcSecurity.zip && rm RpcSecurity.zip \ 
  && unzip -q -d /opt/node/neo-cli RpcSystemAssetTracker.zip && rm RpcSystemAssetTracker.zip \ 
  && unzip -q -d /opt/node/neo-cli RpcWallet.zip && rm RpcWallet.zip \ 
  && unzip -q -d /opt/node/neo-cli SimplePolicy.zip && rm SimplePolicy.zip \ 
  && unzip -q -d /opt/node/neo-cli StatesDumper.zip && rm StatesDumper.zip

ADD ./configs/protocol.json /opt/node/neo-cli/protocol.json
ADD ./configs/config.json /opt/node/neo-cli/config.json
ADD ./configs/plugins/appLogConfig.json /opt/node/neo-cli/Plugins/ApplicationLogs/config.json
ADD ./configs/plugins/importBlocks.json /opt/node/neo-cli/Plugins/ImportBlocks/config.json
ADD ./configs/plugins/rpcNep5Tracker.json /opt/node/neo-cli/Plugins/RpcNep5Tracker/config.json
ADD ./configs/plugins/rpcSecurity.json /opt/node/neo-cli/Plugins/RpcSecurity/config.json
ADD ./configs/plugins/rpcSystemAssetTracker.json /opt/node/neo-cli/Plugins/RpcSystemAssetTracker/config.json
ADD ./configs/plugins/simplePolicyConfig.json /opt/node/neo-cli/Plugins/SimplePolicy/config.json
ADD ./configs/plugins/statesDumper.json /opt/node/neo-cli/Plugins/StatesDumper/config.json

ADD ./scripts/run.sh /opt/
ADD ./scripts/start.sh /opt/

CMD ["/bin/bash", "/opt/run.sh"]