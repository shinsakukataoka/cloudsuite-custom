FROM cloudsuite/cassandra:4.1.0

ENV YCSB_VERSION 0.17.0

RUN apt-get update && apt-get install -y git && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/shinsakukataoka/ycsb-0.17.0.git /ycsb

COPY setup_tables.txt /setup_tables.txt
COPY warmup.sh /warmup.sh
COPY load.sh /load.sh
RUN chmod +x /load.sh /warmup.sh
