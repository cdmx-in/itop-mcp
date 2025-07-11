# iTop MCP Server

A Model Context Protocol (MCP) server for integrating with iTop ITSM (IT Service Management) systems. This server provides AI assistants with the ability to interact with iTop through its REST API, enabling operations like ticket management, CI (Configuration Item) management, and more.

## 🚀 Features

The iTop MCP server provides the following tools:

**Enhanced Support Ticket Management:**
- **get_support_tickets**: Get support tickets with SLA tracking and optimized field selection
- **get_ticket_details**: Get comprehensive details for a specific ticket
- **create_user_request**: Streamlined user request creation with smart field resolution
- **search_tickets_by_caller**: Find tickets by caller name
- **get_my_assigned_tickets**: Get tickets assigned to a specific agent with status grouping

**Core iTop Operations:**
- **list_operations**: List all available iTop REST API operations
- **get_objects**: Search and retrieve iTop objects (tickets, users, CIs, etc.)
- **create_object**: Create new objects in iTop
- **update_object**: Update existing objects
- **delete_object**: Delete objects (with simulation mode for safety)
- **apply_stimulus**: Apply state transitions to objects (e.g., resolve tickets)
- **get_related_objects**: Find related objects through impact/dependency relationships
- **check_credentials**: Verify iTop API credentials

**Organization Management:**
- **get_organizations**: List and search organizations with filtering

**AI & Smart Query Features:**
- **smart_query_processor**: Use natural language to query iTop data, including advanced stats, grouping, SLA/time analysis, and multi-query comparison.
- **Dynamic Schema Discovery**: Automatically detects available iTop classes and fields, so you don't need to hardcode field names.
- **Flexible Output**: Results can be formatted as tables, summaries, JSON, or detailed views.
- **Extensible Tools**: Add new tools by decorating async functions with `@mcp.tool()`.

## Installation

### Option 1: Install from PyPI (Recommended)

```bash
# Install from PyPI
pip install itop-mcp

# Or using uv
uv add itop-mcp
```

### Node.js Implementation

```bash
# Install from npm (coming soon)
npm install itop-mcp-nodejs

# Or clone and build locally
git clone https://github.com/roneydsilva/itop-mcp.git
cd itop-mcp/nodejs
npm install
npm run build
```

## 🔧 MCP Configuration

### Prerequisites

1. **iTop Instance**: Access to an iTop instance with REST API enabled
2. **iTop User Account**: User account with "REST Services User" profile
3. **Environment Variables**: Set the following environment variables:
   ```bash
   export ITOP_BASE_URL="https://your-itop-instance.com"
   export ITOP_USER="your-username"
   export ITOP_PASSWORD="your-password"
   export ITOP_VERSION="1.4"  # Optional, defaults to 1.4
   ```

### Claude Desktop Configuration

Add to your Claude Desktop configuration file:

**For Python implementation:**

```json
{
  "mcpServers": {
    "itop": {
      "command": "python",
      "args": ["-m", "main"],
      "cwd": "/path/to/itop-mcp",
      "env": {
        "ITOP_BASE_URL": "https://your-itop-instance.com",
        "ITOP_USER": "your-username", 
        "ITOP_PASSWORD": "your-password",
        "ITOP_VERSION": "1.4"
      }
    }
  }
}
```

**For installed package:**

```json
{
  "mcpServers": {
    "itop": {
      "command": "itop-mcp",
      "env": {
        "ITOP_BASE_URL": "https://your-itop-instance.com",
        "ITOP_USER": "your-username",
        "ITOP_PASSWORD": "your-password", 
        "ITOP_VERSION": "1.4"
      }
    }
  }
}
```

**For Node.js implementation:**

```json
{
  "mcpServers": {
    "itop": {
      "command": "node",
      "args": ["dist/index.js"],
      "cwd": "/path/to/itop-mcp/nodejs",
      "env": {
        "ITOP_BASE_URL": "https://your-itop-instance.com",
        "ITOP_USER": "your-username",
        "ITOP_PASSWORD": "your-password",
        "ITOP_VERSION": "1.4"
      }
    }
  }
}
```

### Other MCP Clients

For other MCP clients, use similar configuration with the appropriate command and environment variables.

## 🎯 Support Ticket Management

The enhanced support ticket functionality provides optimized field selection for common ITSM operations:

### Default Fields for UserRequest:
- `ref`: Ticket reference number
- `title`: Ticket title/summary
- `status`: Current status
- `start_date`: Ticket start date
- `close_date`: Ticket close date  
- `sla_tto_passed`: SLA Time to Own compliance (✓/✗)
- `sla_ttr_passed`: SLA Time to Resolve compliance (✓/✗)

### SLA Tracking
The server automatically tracks SLA compliance and provides visual indicators:
- ✅ **On Time**: SLA target met
- ❌ **Breached**: SLA target exceeded  
- ➖ **N/A**: SLA not applicable

### Output Formats
1. **detailed**: Full ticket information with SLA status
2. **summary**: Condensed view with status breakdown and SLA breach count
3. **table**: Tabular format for easy scanning

## 🧪 Development & Testing

### Running Tests

```bash
# Run all tests
python tests/run_tests.py

# Run specific test types
python tests/run_tests.py --unit        # Unit tests only
python tests/run_tests.py --live        # Live tests only (requires iTop instance)
python tests/run_tests.py --nodejs      # Node.js tests only
python tests/run_tests.py --lint        # Linting only

# Auto-fix linting issues
python tests/run_tests.py --fix
```

### Code Quality

The project includes comprehensive linting and formatting:

- **Black**: Code formatting
- **isort**: Import sorting  
- **Flake8**: Code linting
- **mypy**: Type checking (Python)
- **ESLint**: TypeScript linting (Node.js)

### Live Testing

Set environment variables and run live tests against your iTop instance:

```bash
export ITOP_BASE_URL="https://your-itop-instance.com"
export ITOP_USER="your-username"
export ITOP_PASSWORD="your-password"

python tests/test_live.py
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Run tests: `python tests/run_tests.py`
5. Submit a pull request

## 📋 Example Usage

Once configured, you can ask Claude:

- "Show me all new support tickets with SLA status"
- "Get user requests that have breached SLA"
- "List incidents by priority with table format"
- "Find tickets assigned to John Smith"
- "Create a new user request for printer issues"

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🔗 Links

- **Repository**: https://github.com/roneydsilva/itop-mcp
- **PyPI Package**: https://pypi.org/project/itop-mcp/
- **Issues**: https://github.com/roneydsilva/itop-mcp/issues
- **iTop Documentation**: https://www.itophub.io/wiki/page?id=latest%3Aadvancedtopics%3Arest_json
   curl -LsSf https://astral.sh/uv/install.sh | sh
   
   # Clone and install
   git clone https://github.com/roneydsilva/itop-mcp.git
   cd itop-mcp
   uv sync
   ```

3. **Configure iTop connection**:
   ```bash
   # Copy the example configuration
   cp .env.example .env
   
   # Edit the .env file with your iTop details
   nano .env
   ```

   Required environment variables:
   - `ITOP_BASE_URL`: Your iTop instance URL (e.g., https://itop.yourcompany.com)
   - `ITOP_USER`: Username with REST Services User profile
   - `ITOP_PASSWORD`: Password for the user
   - `ITOP_VERSION`: API version (optional, default: 1.4)

## Usage

### Running the Server

```bash
# Activate the virtual environment
source .venv/bin/activate

# Run the server
uv run main.py
```

### Connecting to Claude Desktop

#### Option 1: Using PyPI Installation

To use this server with Claude Desktop, add the following to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "itop": {
      "command": "itop-mcp",
      "env": {
        "ITOP_BASE_URL": "https://your-itop-instance.com",
        "ITOP_USER": "your_username",
        "ITOP_PASSWORD": "your_password"
      }
    }
  }
}
```

#### Option 2: Using Source Installation

```json
{
  "mcpServers": {
    "itop": {
        "command": "uv",
        "args": [
            "run",
            "--directory",
            "/path/to/itop-mcp",
            "itop-mcp"
        ],
        "env": {
            "ITOP_BASE_URL": "https://your-itop-instance.com",
            "ITOP_USER": "your_username",
            "ITOP_PASSWORD": "your_password",
            "ITOP_VERSION": "1.3"
        }
    }
  }
}
```

> **Note**: This works because we've configured `itop-mcp` as an entry point in `pyproject.toml`. You need to run this from the project directory where `pyproject.toml` is located, or uv needs to be able to find the project.
```

### Example Operations

Once connected, you can ask your AI assistant to perform operations like:

**Basic Operations:**
- "List all open user requests in iTop"
- "Create a new incident ticket for server downtime"
- "Find all CIs related to the mail server"
- "Update the priority of ticket #123 to high"
- "Resolve ticket #456 with resolution details"

**Enhanced Queries:**
- "Get the latest 5 tickets created today"
- "Show me all tickets assigned to John Smith"
- "Find all tickets reported by Jane Doe"
- "Get detailed information for ticket R-000123"
- "List organizations containing 'Tech' in their name"

**Smart Ticket Creation:**
- "Create a new user request for printer issues reported by John from IT Department"

**AI-Powered Smart Queries:**
- "Get me PC count"
- "Give me status-based stats for the PCs"
- "Get me active tickets generated by PC-wise"
- "Change requests completed vs not completed on time"
- "Tickets closed vs not closed on time based on SLA"
- "List all servers in the production environment"
- "Show me all virtual machines running"

## iTop Class Examples

Common iTop classes you can work with:

- **UserRequest**: User requests/tickets
- **Incident**: Incident tickets
- **Person**: Users and contacts
- **Organization**: Organizations/companies
- **Server**: Server configuration items
- **Application**: Application configuration items
- **Service**: IT services
- **Contract**: Contracts and SLAs

## Advanced Features (Updated July 2025)

This server now supports advanced, AI-powered natural language queries and smart schema discovery. Key features include:

- **Smart Query Processor**: Use natural language to ask for any iTop data (e.g., "Show all virtual machines running", "List all servers in production", "Tickets closed vs not closed on time based on SLA").
- **Automatic Class & Field Detection**: The server dynamically discovers iTop classes and fields, so you don't need to hardcode field names.
- **Flexible Output**: Results can be formatted as tables, summaries, JSON, or detailed views.
- **SLA & Time Analysis**: Supports queries about SLA compliance, overdue tickets, and on-time completion.
- **Multi-Query Comparison**: Easily compare stats (e.g., closed vs not closed, completed on time vs not on time).
- **Relationship & Grouping**: Group results by status, organization, or any field, and link related objects (e.g., network devices with locations).
- **Extensible Tools**: Add new tools by decorating async functions with `@mcp.tool()`.

### Example Smart Queries

- "Get me PC count"
- "Give me status-based stats for the PCs"
- "Get me active tickets generated by PC-wise"
- "Change requests completed vs not completed on time"
- "Tickets closed vs not closed on time based on SLA"
- "List all servers in the production environment"
- "Show me all virtual machines running"

### How it Works

- The main server logic is in `main.py`.
- Uses a class taxonomy and dynamic schema discovery to map natural language to iTop REST API queries.
- Handles errors gracefully and provides suggestions if a query returns no results.
- Supports both simple and complex queries, including grouping, filtering, and comparisons.

---

## Security Notes

- Always use HTTPS for your iTop instance in production
- Store credentials securely (use environment variables, not hardcoded values)
- The user account should have minimal necessary permissions
- Test operations in a development environment first
- Use simulation mode for delete operations until you're confident

## Troubleshooting

### Common Issues

1. **Authentication errors**: Ensure your user has the "REST Services User" profile in iTop
2. **Connection errors**: Verify the ITOP_BASE_URL is correct and accessible
3. **Permission errors**: Check that the user has appropriate rights on the objects you're trying to access

### Testing the Connection

Use the `check_credentials` tool to verify your configuration:

```python
# The server will automatically test credentials on startup
# You can also ask the AI assistant: "Check my iTop credentials"
```

## Development

To extend the server:

1. Add new tools by creating functions decorated with `@mcp.tool()`
2. Follow the iTop REST API documentation for available operations
3. Handle errors gracefully and provide informative messages
4. Test thoroughly in a development environment
5. Use the smart query processor for rapid prototyping and testing of new query types

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

This project is open source. See the LICENSE file for details.

## References

- [Model Context Protocol Documentation](https://modelcontextprotocol.io/)
- [iTop REST API Documentation](https://www.itophub.io/wiki/page?id=latest:advancedtopics:rest_json)
- [iTop Official Website](https://www.combodo.com/itop)