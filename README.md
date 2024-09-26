# agl-repository-template
Template for Repository using a Flake Setup.

## Setup
Build the app with `nix build`, then run the app using `nix run`

## Running Django Production Server via script
'poetry run django-server' in terminal
- see script definition in pyproject.toml (Run in Django Project root)

## The Ten Steps to understanding AGL Repositories

### 1. It is convention to use - in the package name and _ in the source code repository.

This ensures code readability. Also referencing errors are minimized.

### 2. All inputs are managed through the flake.nix. This serves as an interface for the Flakes defined in nix-config.

flake.nix is always the place to look first regarding the inputs. You can trace flake imports down by looking at /home/agl-admin/nix-config/flake.nix first. Nix-config is the place for Networking, locally installed services as well as hardware quirks. If it is deployed, you will reference your API through nix-config to run as a background service on the clinic servers or study laptops.

### 3. Gunicorn is used for launching the application server in deployment

Deploys the services, makes workers for automation for this template. Define the application port and hostname here. (This is for after development. Gunicorn is configured in agl_repository_template/run_gunicorn.py)

### 4. Poetry is used for python dependency management

Poetry manages Python dependencies through the pypoetry.toml file.

### 5. Nix is used to launch virtual environments and to manage package dependencies. This ensures clean builds.

Packages can be directly downloaded from the nix store. These are imported through flake.lock. By running flake lock, your flake.lock is locked and updated according to your flake.nix. Here, some of the packages impoerted are: cuda dependencies, c language support.

### 6. No Github no Nix

Push all changes regularly, to ensure they are used in production.

### 7. Django Unless Overkill

Django us preferrably used for repositories. This ensures interchangeability as well as full stack functionality.

### 8. RESTful API's make nice systemmd services

To ensure the services can communicate appropriately. Django REST Framework is used to provide the functionality. Repositories are referenced

### 9. Reduce manual imports using PyPi

Could your repository be an import? Maybe a full stack django API is not necessary. Make your repository a python package by uploading it to PyPi and then referencing it through Poetry. 

### 10. VS Code Extensions you should download

Repositories are easier to understand when these extensions are installed: Nix Language Support, Python, Django, GitHub Repositories.
