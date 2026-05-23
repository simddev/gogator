# gator

A multi-user RSS feed aggregator CLI written in Go. Add feeds, follow other users' feeds, and browse posts — all from your terminal, backed by PostgreSQL.

## Prerequisites

- [Go](https://go.dev/doc/install) 1.22+
- [PostgreSQL](https://www.postgresql.org/download/) 15+

## Installation

```bash
go install github.com/simddev/gogator@latest
```

## Setup

**1. Create a PostgreSQL database:**

```bash
psql -U postgres -c "CREATE DATABASE gogator;"
```

**2. Create the config file at `~/.gatorconfig.json`:**

```json
{
  "db_url": "postgres://postgres:yourpassword@localhost:5432/gogator?sslmode=disable"
}
```

**3. Run the database migrations** (requires [goose](https://github.com/pressly/goose)):

```bash
cd sql/schema
goose postgres "postgres://postgres:yourpassword@localhost:5432/gogator" up
```

## Usage

**Register and log in:**

```bash
gator register alice
gator login alice
```

**Add and follow feeds:**

```bash
gator addfeed "Boot.dev Blog" "https://www.wagslane.dev/index.xml"
gator addfeed "Hacker News" "https://news.ycombinator.com/rss"
gator follow "https://techcrunch.com/feed/"
```

**Start the aggregator** (runs continuously, fetching new posts):

```bash
gator agg 1m
```

**Browse posts:**

```bash
gator browse       # shows 2 most recent posts
gator browse 10    # shows 10 most recent posts
```

**Other commands:**

```bash
gator users              # list all users
gator feeds              # list all feeds
gator following          # list feeds you follow
gator unfollow <url>     # unfollow a feed
gator reset              # delete all users (development only)
```
