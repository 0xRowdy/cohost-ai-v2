## FEATURE:

Build an AI-powered virtual co-host agent service for CoHost AI that automates guest communication for short-term rental properties. The service should handle real-time guest interactions across multiple STR platforms while maintaining property-specific context and professional communication standards.

**Core Functionality:**

- **Guest Communication Automation**: Handle guest inquiries, booking confirmations, check-in/check-out instructions, and general support messages across Airbnb, Vrbo, Guesty, Hostaway, and Turno platforms
- **Context-Aware Responses**: Understand property-specific details, guest booking information, conversation history, and maintain state across multi-turn conversations
- **Template-Based Messaging**: Use customizable message templates while maintaining natural conversation flow with property manager's brand voice
- **Intelligent Escalation**: Identify complex issues, emergencies, or complaints requiring human intervention and route them appropriately with immediate notifications
- **Multi-Property Support**: Handle communications for multiple properties simultaneously with property-specific knowledge and house rules
- **Performance Optimization**: Cache common responses, track AI usage costs, and optimize response times for high-volume properties

## TOOLS:

- **Message Generation Service**: Generate contextual responses using ChatGPT/Gemini APIs with property details, guest booking info, and conversation history as context
- **Template Management Engine**: CRUD operations for message templates with Zod validation, supporting variables like guest name, property name, check-in codes, etc.
- **Guest Context Retrieval**: Query Convex database for guest booking details, property information, previous conversation history, and escalation flags
- **Sentiment Analysis Tool**: Analyze guest message tone and urgency to determine priority levels and escalation triggers
- **Multi-Platform Messaging Gateway**: Send messages through integrated STR platform APIs with webhook handling for incoming messages
- **File Upload Handler**: Process property images, documents, and training materials via UploadThing with automatic optimization
- **Email Notification Service**: Send alerts to property managers via Resend for urgent issues, escalations, or daily summaries
- **Cache Management**: Store frequently accessed responses and property data in Redis with TTL policies
- **Date/Time Processing**: Handle booking dates, check-in/out times, and timezone conversions using date-fns
- **Performance Monitoring**: Track response times, error rates, and AI costs using Sentry and PostHog integration

## DEPENDENCIES

- **AI Models**: ChatGPT API key and/or Google Gemini API credentials with rate limiting configuration
- **Database**: Convex real-time database connection for conversations, templates, properties, and guest data
- **Authentication**: Clerk session tokens for property manager access control and team permissions
- **Caching**: Redis connection string for response caching and session management
- **Email Service**: Resend API key for system notifications and escalation alerts
- **File Storage**: UploadThing API keys for property asset management
- **STR Platform APIs**: Airbnb, Vrbo, Guesty, Hostaway, and Turno API credentials and webhook endpoints
- **Monitoring**: Sentry DSN for error tracking and PostHog API key for user analytics
- **State Management**: TanStack Query for client/server state synchronization
- **Validation**: Zod schemas for API payloads, form inputs, and AI response validation
- **Date Processing**: date-fns library for timezone-aware date handling
- **TypeScript Types**: Custom types for STR platform data models, AI responses, and property schemas
- **Environment Variables**: Secure storage for all API keys, connection strings, and configuration settings

## SYSTEM PROMPT(S)

**Primary CoHost Agent System Prompt:**

```
You are CoHost AI, a professional virtual assistant specializing in short-term rental guest communication. You represent property managers and must maintain their brand voice while providing exceptional guest service.

CORE RESPONSIBILITIES:
- Respond to guest inquiries with accurate, property-specific information
- Maintain a warm, professional, and helpful tone throughout all interactions
- Provide clear, actionable information for common requests (check-in, WiFi, amenities, local recommendations)
- Use property-specific context including amenities, house rules, check-in procedures, and local timezone

ESCALATION TRIGGERS - Immediately route to human manager for:
- Emergency situations (medical, safety, security concerns)
- Property damage reports or maintenance issues
- Guest complaints requiring refunds or policy exceptions
- Legal or dispute-related communications
- Requests outside established property policies

RESPONSE GUIDELINES:
- Always use guest's name when available
- Include relevant property details (WiFi passwords, door codes, amenities)
- Provide local recommendations when appropriate
- Maintain conversation context throughout guest stay
- Never promise anything outside established property policies
- End responses with offer for additional assistance

PROPERTY CONTEXT VARIABLES:
- Property name, type, and key amenities
- Check-in/out times and procedures
- House rules and policies
- Local timezone and area information
- Emergency contact procedures
- WiFi credentials and door codes
```

**Template Configuration Instructions:**

```
Customize responses based on:
- Property type (apartment, house, cabin, etc.)
- Location and local attractions
- Property manager's communication style preferences
- Seasonal considerations and local events
- Guest demographic and booking details
```

## EXAMPLES:

- **Basic Guest Inquiry Handler**: TypeScript service handling common Q&A with Redis caching for frequent questions
- **Check-in Automation Service**: Automated check-in flow with door codes, WiFi details, and property instructions using date-fns for timing
- **Emergency Escalation Handler**: Sentiment analysis-powered escalation system with immediate Resend email notifications
- **Booking Confirmation Processor**: Webhook-driven service processing STR platform booking confirmations with Convex real-time updates
- **Multi-Property Context Manager**: Service managing simultaneous conversations across multiple properties with property-specific knowledge
- **Template A/B Testing Service**: Testing different message templates for engagement optimization using PostHog analytics
- **File Upload Training Service**: UploadThing integration for property managers to upload custom training materials and property documents
- **Integration Webhook Processor**: Handling incoming messages from multiple STR platform APIs with unified response formatting

## DOCUMENTATION:

- **Framework**: TanStack Start Documentation: https://tanstack.com/start/latest
- **Database**: Convex TypeScript Client: https://docs.convex.dev/client/typescript
- **Authentication**: Clerk TypeScript SDK: https://clerk.com/docs/references/typescript/overview
- **State Management**: TanStack Query Documentation: https://tanstack.com/query/latest
- **Validation**: Zod Schema Validation: https://zod.dev/
- **AI APIs**: OpenAI TypeScript SDK: https://platform.openai.com/docs/libraries, Google AI TypeScript: https://ai.google.dev/tutorials/node_quickstart
- **Email Service**: Resend TypeScript SDK: https://resend.com/docs/send-with-nodejs
- **File Upload**: UploadThing TypeScript Integration: https://docs.uploadthing.com/
- **Caching**: Redis TypeScript Client: https://redis.io/docs/connect/clients/nodejs/
- **Date Handling**: date-fns Documentation: https://date-fns.org/docs/Getting-Started
- **Monitoring**: Sentry Node.js Integration: https://docs.sentry.io/platforms/node/, PostHog TypeScript: https://posthog.com/docs/libraries/node
- **Testing**: Vitest Testing Framework: https://vitest.dev/guide/
- **STR Platform APIs**: Airbnb API, Vrbo Partner API, Guesty Open API, Hostaway API, Turno API documentation

## OTHER CONSIDERATIONS:

- **Cost Optimization**: Implement Redis caching for frequent responses to minimize AI API calls and reduce operational costs
- **Rate Limiting**: Handle AI API rate limits gracefully with exponential backoff and queue management
- **Error Handling**: Implement comprehensive error handling with Sentry integration and graceful fallback to human agents
- **Security**: Validate all STR platform webhooks, sanitize user inputs, and protect guest PII according to platform requirements
- **Performance**: Use TanStack Query caching strategies and Redis for sub-second response times
- **File Management**: Configure UploadThing size/type restrictions for property images and training documents
- **Email Rate Limits**: Manage Resend sending quotas and implement batching for high-volume notifications
- **Real-time Updates**: Leverage Convex's real-time capabilities for live conversation updates and immediate escalations
- **Testing Strategy**: Use Vitest with comprehensive mocking for AI APIs, database calls, and external integrations
- **Environment Configuration**: Use TypeScript environment validation with Zod for all API keys and configuration
- **Data Retention**: Implement policies for conversation history, guest data cleanup, and GDPR compliance
- **Scalability**: Design for multi-tenant architecture supporting thousands of properties and concurrent conversations
- **Monitoring**: Track AI response quality, user satisfaction scores, and system performance metrics
- **Deployment**: Consider serverless deployment patterns compatible with Convex and real-time requirements
- **Backup Strategy**: Ensure all AI training data, templates, and conversation history are properly backed up
- **Multi-language Support**: Design architecture to support internationalization for global property portfolios
