FROM python:3.7

RUN pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple && pip install six psutil lxml pyopenssl --no-cache-dir

RUN wget "https://packages.microsoft.com/config/debian/11/packages-microsoft-prod.deb" -O packages-microsoft-prod.deb && dpkg -i packages-microsoft-prod.deb && rm packages-microsoft-prod.deb

RUN sed -i -e "s/deb.debian.org/mirrors.tuna.tsinghua.edu.cn/" /etc/apt/sources.list && apt-get update && apt-get install -y powershell

RUN curl -L 'https://developer.vmware.com/docs/17484/' \
  -H 'authority: developer.vmware.com' \
  -H 'accept: text/html' \
  -H 'referer: https://developer.vmware.com/powercli/installation-guide' \
  -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.0.0 Safari/537.36' \
  --compressed \
  -o VMware-PowerCLI-13.0.0-20829139.zip

SHELL ["/usr/bin/pwsh", "-c"]

RUN cd $($env:PSModulePath | awk -F ':' '{print $1}') && \
    mv /VMware-PowerCLI-13.0.0-20829139.zip . && \
    Expand-Archive ./VMware-PowerCLI-13.0.0-20829139.zip ./ && \
    rm -rf ./VMware-PowerCLI-13.0.0-20829139.zip

ENTRYPOINT pwsh