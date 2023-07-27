# Tracking the Execution Status of Workflows

This repository provides a base schema for capturing workflow execution status data. It can be tailored according to the requirements of the underlying technology and is aimed to be used both for playbooks and workflows executed manually, automatically or in a hybrid manner. In addition, [section 2](#2-refined-schema-for-oasis-cacao-security-playbooks) provides a refined version of the schema aimed to be used with the [OASIS CACAO Playbooks Standard](https://www.oasis-open.org/committees/cacao). Finally, [section 3](#3-json-validation-schema) provides a JSON validation schema for the refined approach presented in [section 2](#2-refined-schema-for-oasis-cacao-security-playbooks).


`PLACEHOLDER: Add image with pseudo-implementation`

### Table of Content
- [Tracking the Execution Status of Workflows](#tracking-the-execution-status-of-workflows)
    - [Table of Content](#table-of-content)
  - [1. Execution Status Schema](#1-execution-status-schema)
  - [1.1 Execution Status Enumeration](#11-execution-status-enumeration)
  - [2. Refined Schema for OASIS CACAO Security Playbooks](#2-refined-schema-for-oasis-cacao-security-playbooks)
  - [2.1 Refined Execution Status Enumeration](#21-refined-execution-status-enumeration)
  - [3. JSON Validation Schema](#3-json-validation-schema)


## 1. Execution Status Schema
| Property Name | Description|
| :--- | :--- |
| type (required) | This property identifies the semantic type of the object. The value of this property is a string and **MUST** be `execution-status`. |
| id (required) | A identifier that uniquely identifies this object. |  
| workflow_step (required)| The identifier of the step in a workflow that this object refers to (tracks). |  
| start_time (required) | A timestamp that identifies the time the step execution started. | 
| duration (optional) | A number (𝕎 - whole number) that represents the amount of time in milliseconds that this step required to be fully performed. |
| status (required) | This property identifies the execution status of the workflow step. The value of this property **SHOULD** come from the `execution-status-enum` enumeration. |  
| status_text (optional) | A description that provides more details pertinent to the execution status of the workflow step. |  
| executed_by (optional) | The entity executed the workflow step. This can be an organization, a team,  or a role, a defence component, etc. |  
| command_b64 (required) | A list of Base64 encodings of the commands that were invoked during the execution of a workflow step, including any values stemming from variables. These are the actual commands executed. |  
| notes (optional) | This property allows incorporating notes (more context) pertinent to the execution of the workflow step. |  
| automated_execution (required) | This property identifies if the workflow step was executed manually or automatically. It is either `true` or `false`. |

## 1.1 Execution Status Enumeration
**Vocabulary Name:** `execution-status-enum`
| Property Name | Description|
| :--- | :--- |
| successfully_executed | The workflow step was executed successfully (completed). |
|failed| The workflow step failed. |
|ongoing| The workflow step is in progress. |
|server_side_error| A server-side error occurred. |
|client_side_error| A client-side error occurred.|
|timeout_error| A timeout error occurred. |
|exception_condition_error| A exception condition error occured. |

## 2. Refined Schema for OASIS CACAO Security Playbooks
For the definitions of the data types, please check the CACAO specification.

| Property Name |Data Type| Description|
| :--- | :--- |:--- |
| type (required) |string| This property identifies the semantic type of the object. The value of this property **MUST** be `execution-status`. |
| id (required) | identifier |A identifier that uniquely identifies this object (e.g., execution-status–UUIDv4). |  
| workflow_step (required)|identifier| The identifier of the CACAO workflow step this object refers to (tracks). |  
| start_time (required) |timestamp| A timestamp that identifies the time the step execution started. | 
| duration (optional) |integer| A number (𝕎 - whole number) that represents the amount of time in milliseconds that this step required to be fully performed. |
| status (required) |enum| This property identifies the execution status of the workflow step. The value of this property **SHOULD** come from the `execution-status-enum` enumeration. |  
| status_text (optional) |string| A description that provides more details pertinent to the execution status of the workflow step. |  
| executed_by (optional) |identifier| The entity executed the workflow step. This can be an `agent-target` or a STIX 2.1 Identity object id. |  
| command_b64 (required) |list of type string| A list of Base64 encodings of the commands that were invoked during the execution of a workflow step, including any values stemming from variables. These are the actual commands executed. |  
| notes (optional) |string|This property allows incorporating notes (more context) pertinent to the execution of the workflow step. |  
| automated_execution (required) |boolean| This property identifies if the workflow step was executed manually or automatically. It is either `true` or `false`. |

## 2.1 Refined Execution Status Enumeration
**Vocabulary Name:** `execution-status-enum`
| Property Name | Description|
| :--- | :--- |
| successfully_executed | The workflow step was executed successfully (completed). |
|failed| The workflow step failed. |
|ongoing| The workflow step is in progress. |
|server_side_error| A server-side error occurred. |
|client_side_error| A client-side error occurred.|
|timeout_error| A timeout error occurred. The timeout of a CACAO workflow step is specified in the “timeout” property. |
|exception_condition_error| A exception condition error ocurred. A CACAO playbook can incorporate an exception condition at the playbook level and in particular with the "workflow_exception" property. |

## 3. JSON Validation Schema

[Execution status JSON schema](https://github.com/cyentific-rni/workflow-status/blob/main/schema/execution-status.json)
