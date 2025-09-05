# Requirements Document

## Introduction

The Prompt Engineer Web App is a full-stack application that leverages Google Gemini 2.0 Flash as the sole LLM for generating optimized prompts tailored to specific target AI models. The app provides a user-friendly interface for crafting prompts that are optimized for different AI providers (OpenAI, Anthropic, Google, etc.) while following a structured workflow defined in prompt engineer.json.

## Requirements

### Requirement 1

**User Story:** As a prompt engineer, I want to access a web application with a clear home page, so that I understand the app's purpose and can start crafting prompts.

#### Acceptance Criteria

1. WHEN a user visits the home page THEN the system SHALL display a hero section explaining the app's purpose
2. WHEN a user views the home page THEN the system SHALL display a prominent "Start Crafting Prompts" call-to-action button
3. WHEN a user clicks the call-to-action THEN the system SHALL navigate to the API setup page

### Requirement 2

**User Story:** As a user, I want to configure my target AI provider and API settings, so that I can generate prompts optimized for my specific use case.

#### Acceptance Criteria

1. WHEN a user accesses the API setup page THEN the system SHALL display a dropdown for selecting target AI providers
2. WHEN a user selects a provider THEN the system SHALL show available models for that provider (GPT-4o, Claude 3.7 Sonnet, Gemini Pro, etc.)
3. WHEN a user views the API setup page THEN the system SHALL provide an input field for entering their Gemini API key
4. WHEN a user enters an API key THEN the system SHALL store it only in session memory and never persist it
5. WHEN a user completes the setup THEN the system SHALL allow navigation to the prompt crafting page

### Requirement 3

**User Story:** As a prompt engineer, I want to input my task description and generate optimized prompts, so that I can get prompts tailored to my target AI model.

#### Acceptance Criteria

1. WHEN a user accesses the prompt crafting page THEN the system SHALL display a textarea for task description input
2. WHEN a user views the crafting page THEN the system SHALL provide a dropdown to select between reasoning and non-reasoning models
3. WHEN a user fills in their task and preferences THEN the system SHALL enable a "Generate Prompt" button
4. WHEN a user clicks "Generate Prompt" THEN the system SHALL call the backend API with the user's input
5. WHEN the prompt is generated THEN the system SHALL display the result in a glassmorphic response card
6. WHEN displaying the result THEN the system SHALL label it as "Optimized for [Provider] [Model]"

### Requirement 4

**User Story:** As a system, I want to use Google Gemini 2.0 Flash exclusively for prompt generation, so that all prompts are generated consistently through one LLM.

#### Acceptance Criteria

1. WHEN the backend receives a prompt generation request THEN the system SHALL use only Gemini 2.0 Flash (gemini-2.0-flash-latest)
2. WHEN calling Gemini API THEN the system SHALL use the endpoint POST https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash-latest:generateContent
3. WHEN making API calls THEN the system SHALL include proper headers with Content-Type and Authorization
4. WHEN generating prompts THEN the system SHALL embed target provider-specific context in the generation request

### Requirement 5

**User Story:** As a system, I want to integrate with the prompt engineer.json workflow, so that I can select appropriate templates and adjust prompts based on target providers.

#### Acceptance Criteria

1. WHEN processing a prompt request THEN the system SHALL read prompt engineer.json to determine the correct workflow
2. WHEN a target provider is selected THEN the system SHALL choose the appropriate sub-workflow (OpenAI, Anthropic, Google, or Other Models Prompt Engineer)
3. WHEN generating prompts THEN the system SHALL adjust templates based on target provider and reasoning vs non-reasoning requirements
4. WHEN workflow selection occurs THEN the system SHALL ensure compatibility with the user's selected model type

### Requirement 6

**User Story:** As a user, I want the application to be secure and performant, so that my API keys are protected and the app responds quickly.

#### Acceptance Criteria

1. WHEN a user enters API keys THEN the system SHALL store them only in session memory
2. WHEN the session ends THEN the system SHALL automatically clear all stored API keys
3. WHEN the backend processes requests THEN the system SHALL act as an API proxy to securely handle Gemini API calls
4. WHEN making external API calls THEN the system SHALL inject the Gemini API key securely without exposing it to the frontend

### Requirement 7

**User Story:** As a user, I want a modern, responsive interface, so that I can use the app effectively on any device.

#### Acceptance Criteria

1. WHEN a user accesses the app on any device THEN the system SHALL display a fully responsive interface
2. WHEN rendering the UI THEN the system SHALL use a modern dark theme with glassmorphic design elements
3. WHEN displaying content THEN the system SHALL ensure mobile-friendly layouts and interactions
4. WHEN users interact with the interface THEN the system SHALL provide smooth animations and transitions

### Requirement 8

**User Story:** As a developer, I want the system to be extensible, so that new AI models and providers can be easily added.

#### Acceptance Criteria

1. WHEN new AI providers are added THEN the system SHALL support them through configuration updates
2. WHEN extending the workflow THEN the system SHALL allow modifications to prompt engineer.json
3. WHEN adding new models THEN the system SHALL integrate them into the existing dropdown structure
4. WHEN the system is deployed THEN it SHALL be ready for production use on platforms like Vercel or Netlify