# Keyhole - MongoDB Performance Analytic
Keyhole is a performance analytics tool, written in GO (Golang), to collect stats from MongoDB instances and to measure performance of a MongoDB cluster.  Moreover, keyhole can read MongoDB full-time diagnostic data (FTDC) data and is [integrated with Grafana's Simple JSON plugin](https://github.com/simagix/keyhole/wiki/MongoDB-FTDC-and-Grafana-Integration) seamlessly.  Golang was chosen to eliminate the needs to install an interpreter or 3pp modules.  [Download executable](https://github.com/simagix/keyhole#download).

With Keyhole, experienced users should be able to spot performance issues and to determine whether upgrades are needed quickly from a few minutes of testing and analyzing the results.  Keyhole supports TLS/SSL connections.

Several features are available, and they are

- **Write Throughputs Test** measures the MongoDB performance by writing documents at a high rate to a MongoDB cluster.
- [**Load test**](docs/LOADTEST.md) extends the *Write throughputs test* by issuing different ops against a MongoDB cluster.  Stats analytic is also provided
  - Memory: resident, virtual, and page faults
  - Executor and ops
  - Latency: read, write, and command
  - Metrics: index keys examined, collection scan, in-memory sort, and ops
  - WiredTiger analytic
- Customized load test with a sample document.  Uses can load test using their own document format (see [LOADTEST.md](docs/LOADTEST.md) for details).
- **Cluster Info** to display information of a cluster including stats to help determine physical memory size.
- [Display all indexes and their usages](https://github.com/simagix/keyhole/wiki/List-All-Indexes-with-Usages)
- [**Seed data**](https://github.com/simagix/keyhole/wiki/Seed-Data-using-a-Template) for demo and educational purposes as a trainer.
- [Display average ops time](https://github.com/simagix/keyhole/wiki/Mongo-Logs-Analytics) and query patterns by parsing logs.

## Use Cases
Refer to [wiki](https://github.com/simagix/keyhole/wiki) for user's guide.

## Usages
### Build
You need `go` installed and use `dep` to pull down dependencies.

```
cd $GOPATH/src
git clone https://github.com/simagix/keyhole.git
cd keyhole

dep ensure
go run keyhole.go --help

go build
./keyhole --help
```

### Download
Download the desired binary.  No other downloads (interpreter or modules) are necessary.

#### Linux
```
curl -L https://github.com/simagix/keyhole/raw/master/build/keyhole-linux-x64 > keyhole ; chmod +x keyhole
```

#### MacOS
Download [keyhole](https://github.com/simagix/keyhole/raw/master/build/keyhole-win-x64.exe) for macOS, or,

```
curl -L https://github.com/simagix/keyhole/raw/master/build/keyhole-osx-x64 > keyhole ; chmod +x keyhole
```

#### Windows
Download [Windows  executable](https://github.com/simagix/keyhole/raw/master/build/keyhole-win-x64.exe).

### Usage
```
$ keyhole --help
```

### Atlas TLS/SSL Mode
An example connecting to Atlas

```
keyhole --info "mongodb+srv://user:secret@cluster0-v7due.gcp.mongodb.net/test"
```

or

```
keyhole --info "mongodb://user:secret@cluster0-shard-00-00-v7due.gcp.mongodb.net:27017,cluster0-shard-00-01-v7due.gcp.mongodb.net:27017,cluster0-shard-00-02-v7due.gcp.mongodb.net:27017/test?replicaSet=Cluster0-shard-0&authSource=admin&ssl=true"
```

### TLS/SSL Mode
```
keyhole --info --sslCAFile /etc/ssl/certs/ca.pem --sslPEMKeyFile /etc/ssl/certs/client.pem "mongodb://user:password@localhost/keyhole?authSource=admin&ssl=true"
```
