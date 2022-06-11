# seedback / dorfplatz.local

A collection of services for local community communication and collaboration

* a (image) board ([nyx](https://github.com/rls-moe/nyx))
* a collaborative document editor ([etherpad](https://etherpad.org))
* a markdown notes and presentation system ([hedgedoc](https://hedgedoc.org))
* a secure chat system ([ssh-chat](https://github.com/shazow/ssh-chat))

## Building and Running

Just use `docker-compose build` to prepare all containers.

Afterwards, `docker-compose up` starts all services and makes them available via `http://localhost:8000`.

The ssh-based chat is exposed via port `9004`.

