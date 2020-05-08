# Dockerized project for VSAQ
### vsaq-docked

This is a skeleton project for working with VSAQ (https://github.com/google/vsaq) an interactive questionnaire application by Google in a Docker environment.

**Note:** This application has not been hardened or vulnerability tested and is not intended for production use.

## Folder Structure
**/srv**
- Custom configuration files to be copyed to container. 
- Contains Dockerfiles and logs

**/vsaq**
- Custom code locaions.
- Base files to customize:
- - /client_side_only_impl = https://github.com/google/vsaq/tree/master/client_side_only_impl
- - /questionnaires = https://github.com/google/vsaq/tree/master/questionnaires
- - /static = https://github.com/google/vsaq/tree/master/vsaq/static

###### Usage
When container starts all files in the ./vsaq folder is copied into the relevant cloned repo locations and the vsaq application is compiled. Changes to these files requires re-running the docker-compose.

**Note:** Changes to CSS files will require a hard reload in the browser to be visible.
