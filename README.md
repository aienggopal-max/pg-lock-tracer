# pg-lock-tracer

eBPF tools for observing PostgreSQL lock activity and contention on Linux. The
toolkit traces heavyweight locks, lightweight locks (LWLocks), row locks, and
spinlock delays. It can also turn a recorded trace into an animated lock graph.

Repository owner: [aienggopal-max](https://github.com/aienggopal-max).
The original project is [jnidzwetzki/pg-lock-tracer](https://github.com/jnidzwetzki/pg-lock-tracer).
This copy updates the README and moves the detailed usage examples to the local guide.

## Install from source

Use Linux with eBPF support and Python 3.10 or newer. On Debian or Ubuntu, install
BCC for the distribution's Python and the build dependencies for `psycopg2`.

```bash
sudo apt install python3-bpfcc python3-venv python3-dev libpq-dev build-essential
git clone https://github.com/aienggopal-max/pg-lock-tracer.git
cd pg-lock-tracer
python3 -m venv --system-site-packages .venv
. .venv/bin/activate
python -m pip install .
```

## Quick start

With PostgreSQL running, set `POSTGRES` to the server binary used by your
instance. The example uses a typical PostgreSQL 18 path on Debian or Ubuntu.
Run a query in another terminal to see lock events. Use `Ctrl+C` to stop tracing.

```bash
POSTGRES=/usr/lib/postgresql/18/bin/postgres
sudo "$PWD/.venv/bin/pg_lock_tracer" -x "$POSTGRES" --statistics
```

To try the visualization with the included sample trace, run this from the
repository root and open `locks.html` in a browser.

```bash
animate_lock_graph -i examples/create_table_trace.json -o locks.html
```

See the [usage guide](docs/usage.md) for command examples and build requirements
for PostgreSQL 14–18, including USDT probes for LWLocks. The
[examples directory](examples/) contains a sample trace and its rendered graph.

## License

[Apache License 2.0](LICENSE). Copyright 2022 Jan Nidzwetzki.
