# identity-server4-docker-support
This project demonstrates how to use Docker to setup and run a simple IdentityServer4 application over ssl.
The project uses the Identity Server 4 Quickstart UI and replaces the in-memory clients with an Entity Framework backing store using SQL Server.

## Technologies
- [.NET Core 3.1](https://dotnet.microsoft.com/download/dotnet-core/3.1)
- [Identity Server 4.1](https://identityserver4.readthedocs.io/en/latest/)
- [Docker 19.03.13](https://www.docker.com/get-started)

## SSL Setup
To run the application over SSL there are a few steps we need to do. In your app root directory run the following commands:

1. ``dotnet dev-certs https --clean``
2. ``dotnet dev-certs https -ep ./conf.d/https/dev_cert.pfx -p <password-i-want-to-use>``
3. ``dotnet dev-certs https --trust``
4. Ensure that the dev_cert.pfx file is available in ./conf.d/https folder. 
5. In your docker-compose.override file update the enviroment variable ``ASPNETCORE_Kestrel__Certificates__Default__Password=<password-i-want-to-use>`` to match the password you entered in step 2.

##  Quick Start

1. Make sure you have Docker installed from [Docker Official Page](https://docs.docker.com/get-docker/)
2. In your app root directory run the following command ``docker-compose build``
3. In your app root directory run the following command  ``docker-compose up``
4. Running ``docker ps`` should now show you two containers ``identityserver`` and ``mcr.microsoft.com/mssql/server`` with their associated port numbers.
5. Browse locally to the ``identityserver`` port to see the `Welcome to IdentityServer4` page.
6. Log in with the test users credentials ``alice/alice`` or ``bob/bob``

##  Container Orchestrator Support

The solution also includes the added container orchestration support files. Fore more information see [Container Tools in Visual Studio](https://docs.microsoft.com/en-us/visualstudio/containers/overview?view=vs-2019)


## Issues
For issues, use the [identity-server4-docker-support issue tracker](https://github.com/ryan-buckman/identity-server4-docker-support/issues).