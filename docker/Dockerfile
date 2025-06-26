FROM python:3.12-slim


RUN apt update && apt install -y git && apt clean
RUN pip install --upgrade pip
RUN pip install mkdocs mkdocs-material

WORKDIR /app/website

# # Ensure SSH is properly configured
RUN --mount=type=secret,id=known_hosts,dst=/root/known_hosts \
    mkdir -p -m 0700 ~/.ssh && \
    cat ~/known_hosts >> ~/.ssh/known_hosts

#Modified repo to resolve disconnection bug
RUN --mount=type=ssh \
    set -ex; \
    git clone https://github.com/sssa-teleoperation/workshop.git;

COPY ./start.sh /start.sh
RUN chmod +x /start.sh 
ENTRYPOINT ["/start.sh"]
