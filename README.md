# Rails 8 Solid Cache

A demonstration application showcasing how to implement and use Solid Cache in a Rails 8 application.

## Features

- Solid Cache integration for high-performance caching
- Example task management interface
- Database-backed cache storage
- Development and production configuration examples

## Prerequisites

- Ruby 3.2.0 or higher
- Rails 8.0.0 or higher
- SQLite3 (or your preferred database)
- Node.js and Yarn for JavaScript dependencies

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/rails_8_solid_cache.git
   cd rails_8_solid_cache
   ```

2. **Install dependencies**
   ```bash
   bundle install
   yarn install
   ```

3. **Set up the database**
   ```bash
   rails db:create db:migrate
   ```

## Configuration

### 1. Configure Cache Database
Update `config/database.yml` to include your cache database configuration:

```yaml
development:
  primary:
    <<: *default
    database: db/development.sqlite3

  cache:
    adapter: sqlite3
    database: db/cache_development.sqlite3
```

### 2. Configure Solid Cache
Update `config/cache.yml`:

```yaml
development:
  store: solid_cache_store
  database: cache
  expires_in: 1.day

production:
  store: solid_cache_store
  database: cache
  expires_in: 1.week
```

### 3. Update Environment Configuration
In `config/environments/development.rb`:

```ruby
config.cache_store = :solid_cache_store
```

## Usage

1. **Enable caching in development**
   ```bash
   rails dev:cache
   ```

2. **Using the cache in your application**
   ```ruby
   # Basic caching
   Rails.cache.fetch('some_key') { 'some_value' }

   # Fragment caching in views
   <% cache @task do %>
     <%= render @task, cached: true %>
   <% end %>
   ```

## Running the Application

```bash
rails server
```

Visit `http://localhost:3000` in your browser.
