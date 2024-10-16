# AI Automation Suggester

An integration for Home Assistant that uses OpenAI's GPT models to analyze your newly added entities and suggest potential automations.

---

## Table of Contents

- [Background and Purpose](#background-and-purpose)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Important Notes](#important-notes)
- [Troubleshooting](#troubleshooting)
- [Roadmap](#roadmap)
  - [Phase 1: Enhanced Entity Analysis](#phase-1-enhanced-entity-analysis)
  - [Phase 2: Interactive Suggestion Management](#phase-2-interactive-suggestion-management)
  - [Phase 3: Automated Automation Creation](#phase-3-automated-automation-creation)
  - [Future Enhancements](#future-enhancements)
  - [Contributing to the Roadmap](#contributing-to-the-roadmap)
  - [Timeline and Updates](#timeline-and-updates)
- [License](#license)
- [Acknowledgments](#acknowledgments)
- [Contributions](#contributions)
- [Disclaimer](#disclaimer)

---

## Background and Purpose

Managing and automating devices in a smart home can be complex, especially as the number of devices grows. The **AI Automation Suggester** integration aims to simplify this process by leveraging OpenAI's GPT models to analyze newly added entities in your Home Assistant setup and provide intelligent automation suggestions. We call it the ultimate 'Matt' mode (only because he's the one who asked for it)

---

## Features

- **Automatic Analysis**: Periodically scans for new entities and analyzes them using AI.
- **Automation Suggestions**: Provides clear and concise suggestions for potential automations.
- **Manual Trigger**: Allows you to manually trigger the AI analysis at any time.
- **Persistent Notifications**: Suggestions are delivered via Home Assistant's persistent notifications.
- **Sensor Entity**: Creates a sensor entity to display the status and suggestions.
- **Configurable Scan Frequency**: Set how often the integration scans for new entities.
- **Supports OpenAI GPT Models**: Uses OpenAI's GPT models for analysis.
- **Local AI Option**: Placeholder for future local AI processing capabilities.

---

## Prerequisites

- **Home Assistant**: Version 2023.5 or later.
- **OpenAI API Key**: You need an OpenAI API key to use the cloud AI processing.

---

## Installation

### 1. **Download the Integration**

- Clone or download the `ai_automation_suggester` repository from GitHub.

### 2. **Copy to Home Assistant**

- Place the `ai_suggester` directory inside the `custom_components` directory of your Home Assistant configuration folder.
  - Your directory structure should look like this:

    ```
    └── config/
        ├── configuration.yaml
        └── custom_components/
            └── ai_suggester/
                ├── __init__.py
                ├── config_flow.py
                ├── const.py
                ├── coordinator.py
                ├── manifest.json
                ├── sensor.py
                ├── services.yaml
                ├── strings.json
                └── translations/
                    └── en.json
    ```

- If the `custom_components` directory doesn't exist, create it.

### 3. **Restart Home Assistant**

- After copying the files, restart Home Assistant to recognize the new integration.

---

## Configuration

### 1. **Add the Integration via Home Assistant UI**

- Navigate to **Settings** > **Devices & Services**.
- Click on **Add Integration**.
- Search for **AI Automation Suggester** and select it.

### 2. **Configure the Integration**

- **Scan Frequency (hours)**: Set how often (in hours) the integration scans for new entities. Default is `24` hours.
- **Use Local AI**: Option to use local AI processing (currently not implemented).
- **OpenAI API Key**: Enter your OpenAI API key. This is required if not using local AI.
- **AI Model**: Select your preferred AI model from the dropdown. Options include:

  - **gpt-3.5-turbo**: Cheap
  - **gpt-4o**: High Quality
  - **o1-mini**: Expensive
  - **gpt-4o-mini**: Recommended
  - **o1-preview**: Very Expensive

  **Note**: The choice of AI model affects the cost and quality of the suggestions. Higher-end models like `gpt-4o-mini` may provide better suggestions but at a higher cost.

### 3. **Obtain an OpenAI API Key**

- Log in or sign up at the [OpenAI Platform](https://platform.openai.com/).
- Navigate to the [API Keys page](https://platform.openai.com/account/api-keys).
- Click on **Create new secret key** and copy the key.
- **Important**: Keep your API key secure and do not share it publicly.

---

## Usage

### 1. **Automatic Suggestions**

- The integration will automatically scan for new entities based on the configured scan frequency.
- When new entities are detected, it will analyze them and create automation suggestions.

### 2. **Manual Trigger**

- You can manually trigger the AI analysis at any time:
  - Go to **Developer Tools** > **Services**.
  - Select `ai_suggester.generate_suggestions` from the list.
  - Click **Call Service**.

### 3. **Viewing Suggestions**

- Suggestions are delivered via Home Assistant's persistent notifications.
- You can also view suggestions in the `sensor.ai_automation_suggestions` entity's attributes.

### 4. **Adding to Lovelace Dashboard**

- You can display the suggestions on your dashboard using an **Entities** card:

  ```yaml
  type: entities
  entities:
    - entity: sensor.ai_automation_suggestions
  ```

---

## Important Notes

### **OpenAI API Key Security**

- **Do Not Share Your API Key**: Keep your OpenAI API key confidential.
- **Revoking Compromised Keys**: If you suspect your API key has been compromised, revoke it immediately and generate a new one.

### **OpenAI API Usage**

- **Costs**: Using the OpenAI API may incur costs. Monitor your usage in the [OpenAI Dashboard](https://platform.openai.com/account/usage).
- **Usage Limits**: Set usage limits in your OpenAI account to avoid unexpected charges.

### **Compatibility**

- **OpenAI Python Library**: The integration requires `openai>=1.0.0`. This is specified in the `manifest.json`.
- **Home Assistant Version**: Ensure you are running Home Assistant version 2023.5 or later.

### **Data Privacy**

- **Data Sent to OpenAI**: The integration sends entity information to OpenAI's API for analysis.
- **User Consent**: By using this integration, you consent to this data being sent to OpenAI.

### **Local AI Processing**

- **Not Yet Implemented**: The option to use local AI is currently a placeholder and not functional.
- **Future Updates**: Stay tuned for updates that may include local AI processing capabilities.

---

## Troubleshooting

### **Common Issues**

1. **OpenAI API Errors**

   - **Symptom**: Error messages related to OpenAI API in notifications or logs.
   - **Solution**:
     - Verify your OpenAI API key is correct.
     - Ensure your API key has not expired or been revoked.
     - Check your OpenAI account for any usage limits or account issues.

2. **Integration Not Showing Up**

   - **Symptom**: After installation, the integration doesn't appear in Home Assistant.
   - **Solution**:
     - Ensure the `ai_suggester` directory is in the correct location.
     - Restart Home Assistant after adding the custom component.
     - Check the logs for any errors during startup.

3. **No Suggestions Generated**

   - **Symptom**: The integration doesn't generate any suggestions.
   - **Solution**:
     - Manually trigger the service `ai_suggester.generate_suggestions`.
     - Check if there are any new entities to analyze.
     - Review logs for any errors during the analysis.

4. **Dependency Issues**

   - **Symptom**: Errors related to the OpenAI Python library version.
   - **Solution**:
     - Ensure that the OpenAI library version is `>=1.0.0`.
     - Clear Home Assistant's cache by deleting the `deps` directory and restart.

### **Logging and Debugging**

- Enable debug logging for more detailed information:

  ```yaml
  logger:
    default: warning
    logs:
      custom_components.ai_suggester: debug
      openai: debug
  ```

- View logs under **Settings** > **System** > **Logs**.

---

## Roadmap

We have an ambitious roadmap for the **AI Automation Suggester** integration to enhance its capabilities and provide even more value to Home Assistant users. Below is a list of planned features and improvements:

---

### **Phase 1: Enhanced Entity Analysis**

#### **1. Comprehensive Integration and Sensor Discovery**

- **Objective**: Extend the integration to analyze all available integrations, sensors, and automations in the user's Home Assistant setup.
- **Details**:
  - Collect detailed information about existing entities and their states.
  - Understand the relationships and dependencies between different entities.
  - Identify potential areas where automations could enhance the smart home experience.

#### **2. Advanced Automation Suggestions**

- **Objective**: Provide more powerful and personalized automation suggestions based on the comprehensive analysis.
- **Details**:
  - Use AI to detect patterns and usage habits.
  - Suggest automations that can improve efficiency, security, and convenience.
  - Include suggestions for energy savings, routine automation, and proactive alerts.

---

### **Phase 2: Interactive Suggestion Management**

#### **1. User Feedback Mechanism**

- **Objective**: Allow users to like or dislike the suggested automations to refine future suggestions.
- **Details**:
  - Implement a user interface where suggestions are listed with options to like or dislike.
  - Use feedback to improve the AI model's understanding of user preferences.
  - Store feedback securely and respect user privacy.

#### **2. Detailed Implementation Guides**

- **Objective**: For liked suggestions, provide concise and clear instructions on how to implement the automation.
- **Details**:
  - Break down the steps required to create the automation within Home Assistant.
  - Include code snippets, configuration examples, and screenshots where applicable.
  - Explain the desired outcome and how the automation enhances the user's smart home.

---

### **Phase 3: Automated Automation Creation**

#### **1. One-Click Automation Deployment**

- **Objective**: Enable users to automatically implement the suggested automations directly from the integration.
- **Details**:
  - Integrate with Home Assistant's automation editor to create automations programmatically.
  - Ensure automations are created following best practices and are easily editable by the user.
  - Provide options for users to review and confirm automations before deployment.

#### **2. Safety and Privacy Measures**

- **Objective**: Implement safeguards to ensure that automations are created securely and do not compromise the user's system.
- **Details**:
  - Include confirmation dialogs and summaries before making changes.
  - Ensure the integration adheres to Home Assistant's security guidelines.
  - Provide options to rollback changes if needed.

---

### **Future Enhancements**

#### **1. Local AI Processing**

- **Objective**: Develop local AI processing capabilities to reduce reliance on cloud services.
- **Details**:
  - Explore the use of local machine learning models compatible with Home Assistant's architecture.
  - Improve response times and reduce costs associated with cloud AI usage.
  - Enhance user privacy by keeping data processing local.

#### **2. Multi-Language Support**

- **Objective**: Support multiple languages to cater to a global user base.
- **Details**:
  - Translate the integration's interface and messages into other languages.
  - Ensure AI-generated suggestions are provided in the user's preferred language.
  - Collaborate with the community for translations and localization efforts.

#### **3. Community Integration Sharing**

- **Objective**: Allow users to share their automations and suggestions with the community.
- **Details**:
  - Create a platform or integrate with existing platforms to share and discover automations.
  - Enable users to benefit from community-driven ideas and solutions.
  - Implement moderation and quality control mechanisms.

---

## Contributing to the Roadmap

We welcome contributions and feedback from the community to help shape the future of the **AI Automation Suggester** integration. If you have ideas, feature requests, or would like to contribute to the development, please open an issue or submit a pull request on our [GitHub repository](https://github.com/yourusername/ai_automation_suggester).

---

## Timeline and Updates

We aim to implement these features progressively, with regular updates provided through the repository. Please check back frequently for the latest news and release notes.

---

**Note:** The features listed in this roadmap are subject to change based on feasibility, user feedback, and ongoing development efforts. Our goal is to provide the most valuable and user-friendly experience possible.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgments

- **Home Assistant Community**: For providing an amazing platform and community support.
- **OpenAI**: For their powerful AI models and APIs.

---

## Contributions

Contributions are welcome! Please open an issue or submit a pull request on GitHub.

---

## Disclaimer

This integration is a third-party custom component and is not affiliated with or endorsed by Home Assistant or OpenAI.

---

# Example Outputs

```yaml
AI Automation Suggestions
Based on the new entities added to your Home Assistant setup, here are some potential automations you could implement:

1. **Media Player Power On/Off Automation**

   - **Trigger**: When any `media_player` entity changes to "on."
   - **Action**: Send a notification to your phone or turn on the corresponding lights in the room where the media player is located (e.g., office, living room).

2. **Scheduled Speaker Activation**

   - **Trigger**: Time-based trigger (e.g., 7:00 AM).
   - **Condition**: Check if `media_player.office_speaker` is off.
   - **Action**: Turn on the `media_player.office_speaker` to play morning news or music.

3. **Media Player Status Notification**

   - **Trigger**: When any `media_player` changes to "off."
   - **Action**: Send a notification to inform you that a specific media player has turned off (e.g., "The living room speaker is now off").

4. **Object Detection Alert**

   - **Trigger**: When `image_processing.front_door_object_detection` or `image_processing.rear_door_object_detection` detects motion.
   - **Action**: Send a notification or trigger a camera to start recording.

5. **Object Detection with Speaker Announcement**

   - **Trigger**: When `image_processing.front_door_object_detection` detects a person.
   - **Action**: Use a media player (e.g., `media_player.office_speaker`) to announce "Someone is at the front door".

6. **DeepStack Object Detection Alert**

   - **Trigger**: When `image_processing.deepstack_object_local_file` detects an object.
   - **Action**: Send a notification with details of the detected object.

7. **Home Security Status Check**

   - **Trigger**: When `image_processing.front_door_object_detection` or `image_processing.rear_door_object_detection` detects an unknown object.
   - **Action**: Turn on all media players in the house to deter intruders.

8. **Presence-based Media Control**

   - **Trigger**: When you arrive home (using presence detection).
   - **Action**: Turn on `media_player.sonos_2` or any other preferred media player and play a welcome playlist.

9. **Room Occupancy Automation**

   - **Trigger**: When a specific media player (e.g., `media_player.denon_avr_x2600h`) turns on.
   - **Action**: Adjust lighting and temperature settings in the corresponding room.

10. **Energy Saving Automation**

    - **Trigger**: When media players have been idle for a certain period.
    - **Action**: Turn them off to save energy.

Feel free to implement these automations to enhance your Home Assistant experience!

```

If you have any questions or need assistance with implementing these suggestions, please feel free to reach out!