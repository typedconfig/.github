# TypedConfig (Tyco)

**TypedConfig (Tyco)** brings type safety, clarity, and maintainability to configuration files. It is a modern configuration language and ecosystem designed to address the pain points of YAML, JSON, TOML, and XML, with a focus on schemas, defaults, and tabular data.

## Key Features

- **Type safety**: Field types and names are defined in the schema and statically enforced.
- **Built-in defaults**: Eliminate repetition without complex nesting or tricky constructs.
- **References and templating**: Define values once, reuse everywhere with automatic updates.
- **Tabular format**: Scan multiple instances at a glance instead of scrolling through verbose key-value pairs.
- **Native comments**: Document your configuration directly in the file.
- **Primary keys and object references**: Use primary keys for lookups and reference other objects by key.

## Why Tyco?

- **Explicit types**: Type declarations are required upfront, avoiding runtime surprises.
- **Structured tabular data**: Designed for tabular configuration, not just nested lists.
- **Real objects, not loose dicts**: Tyco uses real objects with defined attributes and schema validation, while YAML relies on arbitrarily nested dictionaries with unenforced fields.
- **Cleaner syntax**: Minimal braces, brackets, and quotes—just the essentials.
- **No redundancy**: Defaults and templates avoid repetition.
- **Human-readable**: Designed for engineers to read and write.

## Example

```tyco
str timezone: UTC  # this is a global config setting

Application:       # schema defined first, followed by instance creation
  str service:
  str profile:
  str command: start_app {service}.{profile} -p {port.number}
  Host host:
  Port port: Port(http_web)  # reference to Port instance defined below
  - service: webserver, profile: primary, host: Host(prod-01-us)
  - service: webserver, profile: backup,  host: Host(prod-02-us)
  - service: database,  profile: mysql,   host: Host(prod-02-us), port: Port(http_mysql)
                  
Host:
 *str hostname:  # star character (*) used as reference primary key
  int cores:
  bool hyperthreaded: true
  str os: Debian
  - prod-01-us, cores: 64, hyperthreaded: false
  - prod-02-us, cores: 32, os: Fedora

Port:
 *str name:
  int number:
  - http_web,   80  # can skip field keys when obvious
  - http_mysql, 3306
```

## Learn More

- Website: https://typedconfig.com
- GitHub: https://github.com/typedconfig
- Docs: https://typedconfig.com/docs

---

This repository contains the home page and shared community resources for the TypedConfig (Tyco) project. For language-specific bindings and tools, see the repositories in the [typedconfig GitHub organization](https://github.com/typedconfig).