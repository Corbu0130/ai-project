# AI Project: MCP Database Server Integration with Open WebUI

## Overview

This project demonstrates the integration of a Model Context Protocol (MCP) database server with Open WebUI, creating a powerful AI development environment that combines local language model inference with database connectivity capabilities.

## Architecture

The project consists of three main components:

1. **Ollama** - Local language model inference server
2. **Open WebUI** - Web-based chat interface for AI interactions
3. **MCP Database Server** - Custom MCP server providing database connectivity tools

### Component Details

#### Ollama
- **Purpose**: Runs local language models for inference
- **Port**: 11434
- **GPU Support**: NVIDIA GPU acceleration enabled
- **Volume**: Persistent model storage in `.volumes/ollama`

#### Open WebUI
- **Purpose**: Web interface for AI chat interactions
- **Port**: 8500 (mapped to container port 8080)
- **Features**: Modern chat interface with model management
- **Volume**: Persistent data storage in `.volumes/open-web-ui`

#### MCP Database Server
- **Purpose**: Provides database connectivity tools via MCP protocol
- **Port**: 3000
- **Supported Databases**: MySQL, PostgreSQL, SQLite, SQL Server
- **Features**: Query execution, schema inspection, data export

## Prerequisites

- Docker and Docker Compose
- NVIDIA GPU with CUDA support (optional, for GPU acceleration)
- Git

## Quick Start

### 1. Clone the Repository
```bash
git clone <repository-url>
cd ai-project
```

### 2. Configure Database Connection
Edit the MCP server environment file:
```bash
# Edit mcp-database-server/mcp-database-server.env
DATABASE_TYPE=mariadb
DATABASE_HOST=host.docker.internal
DATABASE_NAME=your_database_name
DATABASE_PORT=3306
DATABASE_USER=your_username
DATABASE_PASSWORD=your_password
```

### 3. Start the Services
```bash
docker-compose -f .docker/docker-compose.yml up -d
```

### 4. Access the Applications
- **Open WebUI**: http://localhost:8500
- **MCP Database Server**: http://localhost:3000

## Development Environment

### Using VS Code Dev Container

The project includes a VS Code dev container configuration for seamless development:

1. Install the "Remote - Containers" extension in VS Code
2. Open the project in VS Code
3. When prompted, click "Reopen in Container"
4. The development environment will be set up automatically

### Dev Container Features

- Pre-configured Python and Node.js environments
- Database management extensions
- Git and development tools
- Jupyter notebook support
- SQLite and MySQL syntax highlighting

## Configuration

### Environment Variables

#### MCP Database Server
```env
DATABASE_TYPE=mysql          # Database type: mysql, postgresql, sqlite, sqlserver
DATABASE_HOST=host.docker.internal
DATABASE_NAME=your_database
DATABASE_PORT=3306
DATABASE_USER=your_username
DATABASE_PASSWORD=your_password
```

#### Open WebUI
```env
OLLAMA_BASE_URL=http://ollama:11434
```

### Docker Compose Configuration

The project uses a custom Docker Compose setup with:

- **Network**: `ai-network` for inter-service communication
- **Volumes**: Persistent storage for models and data
- **GPU Support**: NVIDIA GPU passthrough for Ollama
- **Port Mapping**: Exposed ports for external access

## Usage Examples

### Database Operations via MCP

The MCP database server provides tools for:

1. **Query Execution**
   ```sql
   SELECT * FROM users WHERE active = 1;
   ```

2. **Schema Inspection**
   - List all tables
   - Describe table structure
   - View database metadata

3. **Data Export**
   - Export query results to CSV/JSON
   - Generate reports

4. **Business Insights**
   - Add and manage business insights
   - Track data analysis findings

### AI Chat Integration

Open WebUI provides:

- **Model Management**: Download and manage local models
- **Chat Interface**: Interactive conversations with AI
- **Context Management**: Maintain conversation history
- **Multi-model Support**: Switch between different models

## Project Structure

```
ai-project/
├── .devcontainer/          # VS Code dev container configuration
├── .docker/               # Docker Compose configuration
├── .volumes/              # Persistent data storage
├── mcp-database-server/   # Custom MCP server implementation
│   ├── src/              # TypeScript source code
│   ├── docs/             # Documentation
│   ├── examples/         # Usage examples
│   └── data/            # Database files
└── readme.md            # This documentation
```

## Advanced Configuration

### Custom Model Setup

1. Access Open WebUI at http://localhost:8500
2. Navigate to Settings > Models
3. Add your preferred models (e.g., llama2, codellama)
4. Configure model parameters as needed

### Database Integration

The MCP server supports multiple database types:

- **MySQL**: Production-ready relational database
- **PostgreSQL**: Advanced open-source database
- **SQLite**: Lightweight file-based database
- **SQL Server**: Microsoft SQL Server integration

### Security Considerations

- Database credentials are stored in environment files
- Use `.env` files for sensitive configuration
- Implement proper access controls for production use
- Consider using Docker secrets for sensitive data

## Troubleshooting

### Common Issues

1. **GPU Not Available**
   - Ensure NVIDIA drivers are installed
   - Check Docker GPU support: `docker run --rm --gpus all nvidia/cuda:11.0-base nvidia-smi`

2. **Database Connection Failed**
   - Verify database server is running
   - Check network connectivity
   - Validate credentials in environment file

3. **Port Conflicts**
   - Change port mappings in docker-compose.yml
   - Ensure ports 8500, 11434, and 3000 are available

### Logs and Debugging

```bash
# View service logs
docker-compose -f .docker/docker-compose.yml logs

# View specific service logs
docker-compose -f .docker/docker-compose.yml logs mcp-database-server

# Access container shell
docker exec -it mcp-database-server bash
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## Support

For issues and questions:
- Check the troubleshooting section
- Review the MCP database server documentation
- Open an issue on the repository

---

**Note**: This project demonstrates the integration of MCP (Model Context Protocol) servers with Open WebUI, enabling AI applications to interact with databases through a standardized protocol. The MCP database server component is based on the ExecuteAutomation database server implementation.
