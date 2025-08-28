# AAP Job Template Survey Questions

This document provides comprehensive survey question configurations for Ansible Automation Platform (AAP) Job Templates based on the playbooks in this repository.

## Table of Contents
- [System Information Gathering Job Template](#system-information-gathering-job-template)
- [File Operations Job Template](#file-operations-job-template)
- [Implementation Guidelines](#implementation-guidelines)
- [Best Practices](#best-practices)

---

## System Information Gathering Job Template

**Playbook:** `playbooks/system_info_template.yml`  
**Purpose:** Collect comprehensive system information from target hosts  
**Job Template Name:** `System Information Collection`

### Survey Configuration

| Field | Value |
|-------|-------|
| **Survey Name** | System Information Collection Survey |
| **Description** | Configure system information gathering parameters and output options |
| **Survey Enabled** | ✅ Yes |

### Survey Questions

#### Question 1: Target User
```yaml
Variable Name: target_user
Question Text: "Username to check (leave empty for current user)"
Answer Variable Name: target_user
Answer Type: Text
Default Answer: ""
Required: No
Min Length: 0
Max Length: 50
Help Text: "Specify a username to gather information about. Leave blank to use the current executing user."
```

#### Question 2: Log File Path
```yaml
Variable Name: log_file_path
Question Text: "Path to save system info log"
Answer Variable Name: log_file_path
Answer Type: Text
Default Answer: "~/system_info.log"
Required: Yes
Min Length: 1
Max Length: 255
Help Text: "Full path where the system information report will be saved. Ensure the directory exists and is writable."
```

#### Question 3: Include Processes
```yaml
Variable Name: include_processes
Question Text: "Include running processes in report?"
Answer Variable Name: include_processes
Answer Type: Multiple Choice (single select)
Choices:
  - "yes"
  - "no"
Default Answer: "no"
Required: Yes
Help Text: "Include top 20 CPU-consuming processes in the system report. May increase execution time."
```

#### Question 4: Include Network Information
```yaml
Variable Name: include_network
Question Text: "Include network information in report?"
Answer Variable Name: include_network
Answer Type: Multiple Choice (single select)
Choices:
  - "yes"
  - "no"
Default Answer: "yes"
Required: Yes
Help Text: "Include IP address, gateway, and network interface information in the report."
```

#### Question 5: Report Detail Level
```yaml
Variable Name: report_format
Question Text: "Select report detail level"
Answer Variable Name: report_format
Answer Type: Multiple Choice (single select)
Choices:
  - "Standard Report"
  - "Detailed Report"
  - "Summary Only"
Default Answer: "Standard Report"
Required: Yes
Help Text: "Standard: Basic system info | Detailed: Includes all optional data | Summary: Essential info only"
```

#### Question 6: Notification Email
```yaml
Variable Name: notification_email
Question Text: "Email for completion notification (optional)"
Answer Variable Name: notification_email
Answer Type: Text
Default Answer: ""
Required: No
Min Length: 0
Max Length: 100
Help Text: "Email address to receive job completion notification. Leave blank to skip notifications."
```

#### Question 7: Job Execution Tags
```yaml
Variable Name: job_tags
Question Text: "Job execution tags (comma-separated, optional)"
Answer Variable Name: job_tags
Answer Type: Text
Default Answer: ""
Required: No
Min Length: 0
Max Length: 200
Help Text: "Specify Ansible tags to run specific tasks only. Example: 'system,network'"
```

---

## File Operations Job Template

**Playbook:** `playbooks/file_operations_template.yml`  
**Purpose:** Perform various file system operations with safety controls  
**Job Template Name:** `File Operations Manager`

### Survey Configuration

| Field | Value |
|-------|-------|
| **Survey Name** | File Operations Survey |
| **Description** | Configure file system operation parameters with safety controls |
| **Survey Enabled** | ✅ Yes |

### Survey Questions

#### Question 1: Operation Type
```yaml
Variable Name: operation_type
Question Text: "Select file operation to perform"
Answer Variable Name: operation_type
Answer Type: Multiple Choice (single select)
Choices:
  - "1"  # Create file/directory
  - "2"  # Copy file/directory
  - "3"  # Move/rename file/directory
  - "4"  # Delete file/directory
  - "5"  # Change permissions
  - "6"  # Search for files
Choice Labels:
  - "1 - Create file/directory"
  - "2 - Copy file/directory"
  - "3 - Move/rename file/directory"
  - "4 - Delete file/directory"
  - "5 - Change permissions"
  - "6 - Search for files"
Default Answer: "1"
Required: Yes
Help Text: "Select the type of file operation you want to perform on the target systems."
```

#### Question 2: Source Path
```yaml
Variable Name: source_path
Question Text: "Source file/directory path"
Answer Variable Name: source_path
Answer Type: Text
Default Answer: "~/example.txt"
Required: Yes
Min Length: 1
Max Length: 500
Help Text: "Full path to the source file or directory. For create operations, this is where the new file/directory will be created."
```

#### Question 3: Destination Path
```yaml
Variable Name: destination_path
Question Text: "Destination path (for copy/move operations)"
Answer Variable Name: destination_path
Answer Type: Text
Default Answer: "~/backup/"
Required: No
Min Length: 0
Max Length: 500
Help Text: "Target path for copy/move operations. Not required for create, delete, permissions, or search operations."
```

#### Question 4: File Permissions
```yaml
Variable Name: file_permissions
Question Text: "File permissions (octal format)"
Answer Variable Name: file_permissions
Answer Type: Multiple Choice (single select)
Choices:
  - "0644"
  - "0755"
  - "0600"
  - "0700"
  - "0666"
  - "0777"
Choice Labels:
  - "0644 (rw-r--r--) - Standard file"
  - "0755 (rwxr-xr-x) - Executable file"
  - "0600 (rw-------) - Private file"
  - "0700 (rwx------) - Private executable"
  - "0666 (rw-rw-rw-) - World writable file"
  - "0777 (rwxrwxrwx) - World writable executable"
Default Answer: "0644"
Required: Yes
Help Text: "Octal permissions for files/directories. Choose carefully for security."
```

#### Question 5: Search Pattern
```yaml
Variable Name: search_pattern
Question Text: "Search pattern (for search operations)"
Answer Variable Name: search_pattern
Answer Type: Multiple Choice (single select)
Choices:
  - "*.txt"
  - "*.log"
  - "*.conf"
  - "*.yml"
  - "*.yaml"
  - "*.json"
  - "*.xml"
  - "*"
Choice Labels:
  - "*.txt - Text files"
  - "*.log - Log files"
  - "*.conf - Configuration files"
  - "*.yml - YAML files"
  - "*.yaml - YAML files (alt extension)"
  - "*.json - JSON files"
  - "*.xml - XML files"
  - "* - All files"
Default Answer: "*.txt"
Required: No
Help Text: "File pattern to search for. Only used with search operations (option 6)."
```

#### Question 6: Search Directory
```yaml
Variable Name: search_directory
Question Text: "Directory to search in"
Answer Variable Name: search_directory
Answer Type: Text
Default Answer: "~/"
Required: No
Min Length: 0
Max Length: 500
Help Text: "Directory path to search within. Only used with search operations (option 6)."
```

#### Question 7: File Content
```yaml
Variable Name: file_content
Question Text: "Content for new file (if creating)"
Answer Variable Name: file_content
Answer Type: Textarea
Default Answer: "This is a test file created by Ansible"
Required: No
Min Length: 0
Max Length: 2000
Help Text: "Text content to write to new files. Only used with create operations (option 1)."
```

#### Question 8: Safety Confirmation
```yaml
Variable Name: safety_confirmation
Question Text: "I understand the risks of file operations"
Answer Variable Name: safety_confirmation
Answer Type: Multiple Choice (single select)
Choices:
  - "yes"
  - "no"
Choice Labels:
  - "Yes, I understand the risks"
  - "No, cancel operation"
Default Answer: "yes"
Required: Yes
Help Text: "Confirmation that you understand file operations can modify or delete data. Required for all operations."
```

#### Question 9: Backup Before Operation
```yaml
Variable Name: backup_before_operation
Question Text: "Create backup before destructive operations?"
Answer Variable Name: backup_before_operation
Answer Type: Multiple Choice (single select)
Choices:
  - "yes"
  - "no"
Choice Labels:
  - "Yes, create backup"
  - "No, proceed without backup"
Default Answer: "yes"
Required: Yes
Help Text: "Create a backup copy before move/delete operations. Highly recommended for production systems."
```

#### Question 10: Execution Environment
```yaml
Variable Name: execution_environment
Question Text: "Select execution environment"
Answer Variable Name: execution_environment
Answer Type: Multiple Choice (single select)
Choices:
  - "default"
  - "minimal"
  - "custom"
Choice Labels:
  - "Default EE - Standard tools"
  - "Minimal EE - Basic tools only"
  - "Custom EE - Enhanced toolset"
Default Answer: "default"
Required: Yes
Help Text: "Choose the execution environment based on your file operation requirements."
```

---

## Implementation Guidelines

### Setting Up Surveys in AAP

1. **Navigate to Job Templates**
   - Go to Resources → Templates
   - Select your job template
   - Click "Edit"

2. **Enable Survey**
   - Check "Prompt on Launch" for Survey
   - Click "Add Survey"

3. **Add Questions**
   - Use the survey questions provided above
   - Copy the exact variable names to ensure compatibility
   - Set appropriate validation rules

4. **Test Survey**
   - Save and launch the job template
   - Verify all survey questions appear correctly
   - Test with different input combinations

### Variable Mapping

Ensure these survey variables map correctly to your playbook variables:

**System Info Template:**
- `target_user` → playbook `target_user`
- `log_file_path` → playbook `log_file_path`
- `include_processes` → playbook `include_processes`
- `include_network` → playbook `include_network`

**File Operations Template:**
- `operation_type` → playbook `operation_type`
- `source_path` → playbook `source_path`
- `destination_path` → playbook `destination_path`
- `file_permissions` → playbook `file_permissions`
- `search_pattern` → playbook `search_pattern`
- `search_directory` → playbook `search_directory`
- `file_content` → playbook `file_content`

---

## Best Practices

### Security Considerations
1. **Path Validation**: Validate file paths to prevent directory traversal attacks
2. **Permission Restrictions**: Limit available permission options for security
3. **User Confirmation**: Require explicit confirmation for destructive operations
4. **Backup Strategy**: Always recommend backups for production systems

### User Experience
1. **Clear Labels**: Use descriptive choice labels that explain the impact
2. **Helpful Defaults**: Provide safe, commonly-used default values
3. **Contextual Help**: Include help text explaining when each option is used
4. **Progressive Disclosure**: Consider conditional survey questions for complex workflows

### Operational Guidelines
1. **Testing**: Always test surveys in a development environment first
2. **Documentation**: Keep this document updated when playbooks change
3. **Validation**: Implement input validation in both surveys and playbooks
4. **Monitoring**: Monitor job execution logs for survey-related issues

### Error Handling
1. **Input Validation**: Validate survey inputs in playbooks
2. **Graceful Failures**: Handle invalid inputs gracefully with clear error messages
3. **Rollback Procedures**: Document rollback procedures for failed operations
4. **Audit Trail**: Maintain logs of all file operations for compliance

---

## Troubleshooting

### Common Issues
1. **Variable Name Mismatch**: Ensure survey variable names exactly match playbook variables
2. **Permission Errors**: Verify target systems have appropriate permissions
3. **Path Issues**: Check that specified paths exist and are accessible
4. **Network Connectivity**: Ensure AAP can reach target systems

### Support Information
- **Playbook Location**: `/playbooks/` directory in this repository
- **Documentation**: This file (`AAP_Survey_Questions.md`)
- **Version**: Compatible with AAP 2.x and Ansible Core 2.12+

---

*Last Updated: $(date)*  
*Repository: ansible-rhdh-templates*  
*Branch: testahon*
