FROM python:3.7

RUN pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple && pip install six psutil lxml pyopenssl --no-cache-dir

RUN wget "https://packages.microsoft.com/config/debian/11/packages-microsoft-prod.deb" -O packages-microsoft-prod.deb && dpkg -i packages-microsoft-prod.deb && rm packages-microsoft-prod.deb

RUN sed -i -e "s/deb.debian.org/mirrors.tuna.tsinghua.edu.cn/" /etc/apt/sources.list && apt-get update && apt-get install -y powershell

CMD pwsh
