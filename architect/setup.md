# Setup Guide

## Prerequisites

- Visual Studio 2019 or later.
- .NET Framework 4.5.2.
- Microsoft SQL Server.
- Node.js and npm/yarn (for `ClientWeb`).

## Server Components

1. Open `Source Server/DDTank 4.1.sln` in Visual Studio.
2. Restore NuGet packages if necessary.
3. Configure connection strings in the respective project configurations or via the database management tools.
4. Build the solution in `Debug` or `Release` mode.

## Web API (Request)

1. Host the `Request` directory as an ASP.NET application in IIS or use the Visual Studio development server.
2. Ensure `Web.config` is properly configured. Key settings include:
   - `conString`: Main database connection string.
   - `crosszoneString`: Cross-zone database connection string.
   - `ReqPath`: Absolute path to the `Request` directory (e.g., `C:\DDtank\Request`).
   - `LogPath`: Path for game logs.

## Desktop Client (ClientWeb)

1. Navigate to the `ClientWeb` directory:
   ```bash
   cd ClientWeb
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. **Configuration**: Note that `ClientWeb/login.js` contains a hardcoded `host` URL (e.g., `http://s1.plusgames.com.br/...`). This may need to be updated to point to your local `Request` API for development.
4. Start the application:
   ```bash
   npm start
   ```

## Database Setup

1. Use the `.BAK` files in the `Db` directory to restore the databases in SQL Server Management Studio (SSMS):
   - Right-click **Databases** > **Restore Database**.
   - Source: Select **Device** and locate the `.BAK` files.
   - Under **Options**, ensure **Overwrite the existing database (WITH REPLACE)** and **Close existing connections to target database** are checked.
2. Execute any necessary scripts found in `Db/Query`.

## Web Environment (IIS & PHP)

The `Request` component and other web assets may require a specific environment:
- **IIS**: Enable CGI.
- **PHP**: Use PHP **7.4**.
- **Extensions**: Requires **Microsoft Drivers 5.9 for PHP (sqlsrv)** (e.g., `sqlsrv_php.dll`) to communicate with SQL Server.
- **Web Platform Installer**: Recommended for easier installation of PHP dependencies on IIS.
