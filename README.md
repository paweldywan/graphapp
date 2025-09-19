# GraphApp

A .NET console application that demonstrates how to authenticate with Microsoft Graph API using Azure Active Directory and retrieve user profile information.

## Overview

This application uses the Microsoft Graph SDK to:
- Authenticate users via interactive browser authentication
- Retrieve the authenticated user's profile information
- Display user details including display name, user principal name, and user ID

## Prerequisites

- .NET 9.0 SDK or later
- An Azure AD application registration
- Visual Studio 2022 or Visual Studio Code (optional)

## Azure AD App Registration Setup

Before running the application, you need to create an Azure AD app registration:

1. Go to the [Azure Portal](https://portal.azure.com)
2. Navigate to **Azure Active Directory** > **App registrations**
3. Click **New registration**
4. Configure the registration:
   - **Name**: GraphApp (or your preferred name)
   - **Supported account types**: Accounts in this organizational directory only
   - **Redirect URI**: Web - `http://localhost`
5. After creation, note down:
   - **Application (client) ID**
   - **Directory (tenant) ID**
6. Under **API permissions**, ensure the following Microsoft Graph permissions are granted:
   - `User.Read` (should be added by default)

## Configuration

### Environment Variables

Create a `.env` file in the project root directory with the following variables:

```env
CLIENT_ID=your-application-client-id
TENANT_ID=your-directory-tenant-id
```

Replace the placeholder values with your actual Azure AD app registration details.

### Alternative: System Environment Variables

You can also set these as system environment variables instead of using a `.env` file:
- `CLIENT_ID`
- `TENANT_ID`

## Installation

1. Clone or download this repository
2. Navigate to the project directory
3. Restore the NuGet packages:
   ```bash
   dotnet restore
   ```

## Usage

1. Ensure your Azure AD app registration is configured correctly
2. Set up your environment variables (`.env` file or system variables)
3. Run the application:
   ```bash
   dotnet run
   ```
4. A browser window will open for authentication
5. Sign in with your Microsoft account
6. The application will display your user profile information in the console

## Dependencies

This project uses the following NuGet packages:

- **Microsoft.Graph** (v5.93.0) - Microsoft Graph SDK for .NET
- **Azure.Identity** (v1.16.0) - Azure identity authentication library
- **dotenv.net** (v4.0.0) - Environment variable management

## Project Structure

```
graphapp/
├── Program.cs              # Main application entry point
├── graphapp.csproj        # Project file with dependencies
├── graphapp.sln          # Solution file
├── .env                  # Environment variables (you need to create this)
└── README.md            # This file
```

## Code Overview

The application follows these main steps:

1. **Load Configuration**: Reads client ID and tenant ID from environment variables
2. **Setup Authentication**: Configures interactive browser credential with Azure Identity
3. **Create Graph Client**: Initializes Microsoft Graph service client
4. **Authenticate User**: Opens browser for user sign-in
5. **Retrieve Profile**: Calls Microsoft Graph `/me` endpoint
6. **Display Results**: Shows user information in console

## Troubleshooting

### Common Issues

- **Missing environment variables**: Ensure `CLIENT_ID` and `TENANT_ID` are properly set
- **Authentication errors**: Verify your Azure AD app registration configuration
- **Permission errors**: Ensure the `User.Read` permission is granted to your app registration
- **Redirect URI mismatch**: Verify the redirect URI is set to `http://localhost` in your app registration

### Error Messages

- `"Please set CLIENT_ID and TENANT_ID environment variables."` - Configure your environment variables
- `"Error retrieving profile: [error details]"` - Check your Azure AD configuration and network connectivity

## Security Notes

- Never commit your `.env` file to version control
- Keep your client ID and tenant ID secure
- This application uses interactive authentication which is suitable for development and testing scenarios

## License

This project is provided as-is for educational and demonstration purposes.

## Contributing

Feel free to submit issues and pull requests to improve this example application.