FROM microsoft/dotnet:runtime

RUN apt-get update \
  && apt-get install -y libleveldb-dev sqlite3 libsqlite3-dev libunwind8-dev unzip screen \
  && rm -rf /var/lib/apt/lists/*

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

RUN unzip neo-cli-linux-x64.zip && rm neo-cli-linux-x64.zip \
&& unzip ApplicationLogs.zip -d neo-cli && rm ApplicationLogs.zip \ 
&& unzip CoreMetrics.zip -d neo-cli && rm CoreMetrics.zip \ 
&& unzip ImportBlocks.zip -d neo-cli && rm ImportBlocks.zip \ 
&& unzip RpcNep5Tracker.zip -d neo-cli && rm RpcNep5Tracker.zip \ 
&& unzip RpcSecurity.zip -d neo-cli && rm RpcSecurity.zip \ 
&& unzip RpcSystemAssetTracker.zip -d neo-cli && rm RpcSystemAssetTracker.zip \ 
&& unzip RpcWallet.zip -d neo-cli && rm RpcWallet.zip \ 
&& unzip SimplePolicy.zip -d neo-cli && rm SimplePolicy.zip \ 
&& unzip StatesDumper.zip -d neo-cli && rm StatesDumper.zip

ADD ./scripts/run.sh /neo-cli/
ADD ./scripts/start.sh /neo-cli/

CMD ["/bin/bash", "neo-cli/run.sh"]