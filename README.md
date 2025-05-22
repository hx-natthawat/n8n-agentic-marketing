# Agentic Marketing Workflow System

An AI-powered multi-agent system for automated marketing campaign creation, built with n8n workflow automation. The system orchestrates specialized AI agents to deliver comprehensive marketing campaigns from concept to execution.

## 🚀 Overview

This project implements a sophisticated marketing automation system using multiple AI agents, each specialized in different aspects of marketing campaign development. The system can generate complete marketing campaigns including market research, creative concepts, visual designs, content strategies, and PR plans.

## 📋 System Architecture

### Core Components

1. **Campaign AI (Orchestrator)**
   - Central workflow that coordinates all agents
   - Handles user interactions via LINE messaging
   - Manages workflow execution sequence
   - Creates and organizes campaign documents in Google Drive

2. **Marketing Manager Agent**
   - Conducts market research and competitor analysis
   - Defines campaign objectives and strategy
   - Sets KPIs, timeline, and budget allocation
   - Targets audience segmentation

3. **Creative Director Agent**
   - Develops multiple creative concepts
   - Aligns creative strategy with campaign objectives
   - Defines visual direction and messaging
   - Provides channel-specific creative strategies

4. **Graphic Designer Agent**
   - Creates detailed visual design specifications
   - Generates AI image prompts and mockups
   - Defines color palettes and typography
   - Produces platform-specific design assets

5. **Content Creator Agent**
   - Develops content strategies for each platform
   - Creates content calendars and posting schedules
   - Generates copy suggestions and hashtags
   - Provides platform-specific content guidelines

6. **PR & Social Media Agent**
   - Manages social media execution plans
   - Develops comprehensive PR strategies
   - Creates press releases and media outreach plans
   - Coordinates event planning and timelines

## 🛠️ Technical Stack

- **Workflow Engine**: n8n
- **AI Models**: 
  - OpenAI GPT-4 (for agent reasoning)
  - Google Gemini 2.0 Flash (for image generation)
- **Integrations**:
  - LINE Messaging API
  - Google Drive API
  - Google Docs API
- **Language**: JSON workflow definitions

## 📁 Project Structure

```
agentic-mkt-mu/
├── Agentic_Marketing___Campaign_AI.json          # Main orchestrator workflow
├── Agentic_Marketing___Marketing_Manager.json    # Marketing strategy agent
├── Agentic_Marketing___Creative_Director.json    # Creative concept agent
├── Agentic_Marketing___Graphic_Designer.json     # Visual design agent
├── Agentic_Marketing___Content_Creator.json      # Content strategy agent
├── Agentic_Marketing___PR_and_Social_Content.json # PR and social media agent
└── README.md                                      # This file
```

## 🚦 Getting Started

### Prerequisites

1. n8n instance (self-hosted or cloud)
2. API credentials for:
   - OpenAI API
   - Google Drive/Docs
   - LINE Messaging API
   - Google Gemini API

### Quick Start Guide

```bash
# 1. Clone the repository
git clone https://github.com/your-org/agentic-mkt-mu.git
cd agentic-mkt-mu

# 2. Set up n8n (if not already installed)
npm install -g n8n
n8n start

# 3. Access n8n UI
# Open browser at http://localhost:5678
```

### Installation

1. **Import Workflows**
   ```bash
   # In n8n UI, go to Workflows > Import
   # Import files in this order:
   1. Agentic_Marketing___Marketing_Manager.json
   2. Agentic_Marketing___Creative_Director.json
   3. Agentic_Marketing___Graphic_Designer.json
   4. Agentic_Marketing___Content_Creator.json
   5. Agentic_Marketing___PR_and_Social_Content.json
   6. Agentic_Marketing___Campaign_AI.json
   ```

2. **Configure Credentials**
   - Navigate to Credentials in n8n
   - Add OpenAI credentials (API key)
   - Add Google OAuth2 (for Drive/Docs)
   - Add LINE credentials (Channel Access Token)
   - Add Google Gemini credentials

3. **Update Webhook URLs**
   ```javascript
   // In Campaign AI workflow, update:
   const WEBHOOK_URL = "https://your-domain.com/webhook/campaign-request";
   const LINE_WEBHOOK = "https://your-domain.com/webhook/line";
   ```

4. **Test Individual Workflows**
   - Run each workflow with test data
   - Verify agent outputs
   - Check Google Drive integration

### Deployment Options

#### Option 1: Docker Deployment
```yaml
# docker-compose.yml
version: '3.8'
services:
  n8n:
    image: n8nio/n8n
    ports:
      - "5678:5678"
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=admin
      - N8N_BASIC_AUTH_PASSWORD=your-password
      - N8N_ENCRYPTION_KEY=your-encryption-key
    volumes:
      - ./n8n-data:/home/node/.n8n
      - ./workflows:/workflows
```

#### Option 2: Cloud Deployment
- **n8n Cloud**: Direct import via UI
- **AWS/GCP/Azure**: Use container services
- **Heroku**: One-click deployment available

### Usage

1. **Via LINE Bot**:
   ```
   User: Create marketing campaign for Dream JELLY TINT
   Bot: Processing your request...
   Bot: Campaign created! View documents: [Google Drive Link]
   ```

2. **Via API**:
   ```bash
   curl -X POST https://your-n8n.com/webhook/campaign-request \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer YOUR_TOKEN" \
     -d '{
       "campaign_request": {
         "product_name": "Dream JELLY TINT",
         "market": "Premium, 1000 Baht",
         "target_audience": "Women 25-40",
         "marketing_budget": "200,000 Baht",
         "campaign_duration": "8 weeks",
         "channels": ["TIKTOK", "IG", "FACEBOOK"]
       }
     }'
   ```

3. **Via Direct Execution**:
   - Open n8n UI
   - Navigate to Campaign AI workflow
   - Click "Execute Workflow"
   - Input parameters in the form
   - Monitor progress in execution view

## 📊 Workflow Features

### Multi-Language Support
- Automatic language detection from user input
- Responses in user's preferred language
- Internal agent communication in English for consistency

### Quality Assurance
- Built-in approval workflows with feedback loops
- Agent Manager reviews outputs before proceeding
- Maximum 3 revision cycles to ensure quality

### Document Management
- Automatic Google Drive folder creation
- Organized document structure by campaign
- Public sharing links for easy access

### Platform-Specific Content
- Tailored strategies for TikTok, Instagram, Facebook
- Channel-specific design specifications
- Optimized content for each platform's best practices

## 🔧 Configuration

### Environment Variables
Configure these in your n8n instance:
- `OPENAI_API_KEY`: Your OpenAI API key
- `GOOGLE_CLIENT_ID`: Google OAuth client ID
- `LINE_CHANNEL_ACCESS_TOKEN`: LINE bot access token

### Webhook Endpoints
Update these URLs in Campaign AI workflow:
- Campaign request webhook
- LINE messaging webhook

## 📡 API Documentation

### Webhook Request Format

**POST** `/webhook/campaign-request`

Headers:
```json
{
  "Content-Type": "application/json",
  "Authorization": "Bearer YOUR_TOKEN"
}
```

Body:
```json
{
  "campaign_request": {
    "product_name": "string",
    "market": "string",
    "key_features": "string",
    "ingredients": "string (optional)",
    "target_audience": "string",
    "marketing_budget": "string",
    "campaign_duration": "string",
    "channels": ["array of strings"],
    "campaign_type": "string"
  }
}
```

### Response Format

```json
{
  "status": "success",
  "campaign_id": "uuid",
  "google_drive_url": "string",
  "documents": {
    "campaign_objectives": "url",
    "creative_concepts": "url",
    "visual_designs": "url",
    "content_strategy": "url",
    "pr_strategy": "url",
    "social_media_plan": "url"
  },
  "execution_time": "seconds",
  "message": "Campaign created successfully"
}
```

## 🔄 Workflow Data Flow

### Agent Communication Protocol

1. **Input Processing**
   ```
   User Request → Language Detection → Parameter Extraction
   ```

2. **Agent Orchestration**
   ```
   Marketing Manager → Creative Director → Graphic Designer
                    ↓
              Content Creator → PR & Social Media
   ```

3. **Output Aggregation**
   ```
   Individual Outputs → Document Generation → Google Drive → User Response
   ```

### Inter-Agent Data Schema

Each agent passes structured data to the next:

```typescript
interface AgentOutput {
  agent_type: string;
  timestamp: string;
  status: "approved" | "needs_revision";
  data: {
    // Agent-specific output structure
  };
  metadata: {
    execution_time: number;
    revision_count: number;
    language: string;
  };
}
```

## 📈 Example Campaign Request

```json
{
  "campaign_request": {
    "product_name": "Dream JELLY TINT",
    "market": "Premium, priced at 1000 Baht per piece",
    "key_features": "Long-lasting formula with moisturization",
    "target_audience": "Women aged 25-40 who purchase premium cosmetics",
    "marketing_budget": "200,000 Baht",
    "campaign_duration": "Launch in 8 weeks",
    "channels": ["TIKTOK", "IG", "FACEBOOK PAGE"]
  }
}
```

## 🤝 Contributing

This is an internal marketing automation system. For improvements or bug reports, please contact the development team.

## 📄 License

Proprietary - All rights reserved

## 🔍 Troubleshooting

### Common Issues

1. **Workflow Timeout**
   - Increase timeout settings in n8n
   - Check API rate limits
   - Verify network connectivity

2. **Agent Communication Failures**
   - Ensure all credentials are properly configured
   - Check JSON schema compatibility
   - Verify webhook URLs are accessible

3. **Google Drive Permission Errors**
   - Re-authenticate Google OAuth
   - Check folder creation permissions
   - Verify API quotas

### Debug Mode
Enable debug logging in n8n to trace workflow execution:
```bash
export N8N_LOG_LEVEL=debug
```

## 🚀 Advanced Configuration

### Custom Agent Behaviors

Modify agent system prompts in respective workflows:
- Adjust tone and style guidelines
- Add industry-specific knowledge
- Customize approval criteria

### Performance Optimization

1. **Parallel Processing**
   - Enable concurrent agent execution where possible
   - Adjust memory allocation for large campaigns
   - Implement caching for repeated requests

2. **Resource Management**
   - Set appropriate timeouts for each agent
   - Configure retry policies
   - Monitor API usage and costs

### Integration Extensions

The system can be extended with:
- Slack notifications
- Email reporting
- CRM integration
- Analytics dashboards

## 📊 Metrics and Monitoring

### Key Performance Indicators

- Average campaign generation time: ~15-20 minutes
- Success rate: 95%+ with retry logic
- API cost per campaign: $2-5 depending on complexity

### Monitoring Setup

1. Configure n8n metrics export
2. Set up alerting for failures
3. Track API usage across agents
4. Monitor document generation success

## 🔐 Security Considerations

- Store API keys securely in n8n credentials
- Implement access controls for workflows
- Regular audit of permissions
- Encrypt sensitive campaign data

## 🗺️ Roadmap

### Planned Features

- [ ] Instagram Reels and YouTube Shorts support
- [ ] A/B testing recommendations
- [ ] Budget optimization algorithms
- [ ] Real-time campaign performance tracking
- [ ] Integration with advertising platforms

### Version History

- **v1.0** - Initial release with 6 core agents
- **v1.1** - Added language detection and translation
- **v1.2** - Implemented feedback loops and quality checks

## 💡 Best Practices

### Campaign Request Guidelines

1. **Product Information**
   - Provide clear, unique selling propositions
   - Include all relevant features and benefits
   - Specify any regulatory requirements

2. **Target Audience**
   - Be specific about demographics
   - Include psychographic details
   - Mention purchasing behaviors

3. **Budget Allocation**
   - Specify currency and total amount
   - Indicate any constraints or preferences
   - Consider 60/30/10 rule for channel distribution

### Workflow Optimization

1. **Reduce Latency**
   - Pre-warm API connections
   - Cache common responses
   - Use webhook queuing for high volume

2. **Error Handling**
   - Implement exponential backoff
   - Set reasonable retry limits
   - Log all failures for debugging

3. **Cost Management**
   - Monitor token usage per agent
   - Implement request throttling
   - Use model selection based on task complexity

## 📚 Resources

### Documentation
- [n8n Workflow Documentation](https://docs.n8n.io)
- [OpenAI API Reference](https://platform.openai.com/docs)
- [Google Workspace APIs](https://developers.google.com/workspace)

### Support
- Technical Issues: Create issue in project repository
- Feature Requests: Contact development team
- Training Materials: Available in shared drive

## 🙏 Acknowledgments

Built with n8n workflow automation platform and powered by OpenAI and Google AI technologies.

### Special Thanks
- n8n community for workflow automation framework
- OpenAI for GPT-4 language models
- Google for Gemini AI and Workspace APIs
- Development team for system architecture and implementation