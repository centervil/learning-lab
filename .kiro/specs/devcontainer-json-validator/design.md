# Design Document

## Overview

The devcontainer.json Validator is a command-line interface (CLI) tool that validates devcontainer.json files against basic conventions. The tool follows a simple architecture with clear separation of concerns: file handling, JSON parsing, validation logic, and output formatting. It is designed to be lightweight, fast, and provide clear feedback to developers.

## Architecture

The application follows a modular architecture with the following high-level flow:

```
CLI Entry Point → File Reader → JSON Parser → Validator → Result Formatter → Output
```

The tool will be implemented as a Node.js CLI application using TypeScript for type safety and better developer experience.

## Components and Interfaces

### 1. CLI Interface (`cli.ts`)
- **Purpose**: Entry point for the application, handles command-line arguments
- **Responsibilities**:
  - Parse command-line arguments
  - Validate file path argument
  - Orchestrate the validation process
  - Handle top-level error cases
  - Set appropriate exit codes

### 2. File Reader (`fileReader.ts`)
- **Purpose**: Handle file system operations
- **Interface**:
  ```typescript
  interface FileReader {
    readFile(filePath: string): Promise<string>
    fileExists(filePath: string): boolean
  }
  ```
- **Responsibilities**:
  - Check file existence
  - Read file contents
  - Handle file system errors

### 3. JSON Parser (`jsonParser.ts`)
- **Purpose**: Parse and validate JSON structure
- **Interface**:
  ```typescript
  interface JsonParser {
    parse(content: string): DevcontainerConfig | null
    isValidJson(content: string): boolean
  }
  ```
- **Responsibilities**:
  - Parse JSON content
  - Handle JSON syntax errors
  - Return structured data or null on failure

### 4. Validator (`validator.ts`)
- **Purpose**: Core validation logic for devcontainer.json rules
- **Interface**:
  ```typescript
  interface Validator {
    validate(config: DevcontainerConfig): ValidationResult
  }
  
  interface ValidationResult {
    isValid: boolean
    errors: ValidationError[]
  }
  
  interface ValidationError {
    rule: string
    message: string
  }
  ```
- **Responsibilities**:
  - Check for required properties (name, image)
  - Generate specific error messages
  - Return comprehensive validation results

### 5. Output Formatter (`outputFormatter.ts`)
- **Purpose**: Format and display results to the user
- **Interface**:
  ```typescript
  interface OutputFormatter {
    formatSuccess(): string
    formatFailure(errors: ValidationError[]): string
  }
  ```
- **Responsibilities**:
  - Format success messages
  - Format error messages with details
  - Ensure consistent output formatting

## Data Models

### DevcontainerConfig
```typescript
interface DevcontainerConfig {
  name?: string
  image?: string
  [key: string]: any // Allow additional properties
}
```

### ValidationError
```typescript
interface ValidationError {
  rule: string      // e.g., "required-name", "required-image"
  message: string   // Human-readable error message
}
```

### ValidationResult
```typescript
interface ValidationResult {
  isValid: boolean
  errors: ValidationError[]
}
```

## Error Handling

### File System Errors
- **File not found**: Display clear message with the attempted file path
- **Permission errors**: Display appropriate permission error message
- **Other I/O errors**: Display generic file reading error with details

### JSON Parsing Errors
- **Invalid JSON syntax**: Display message indicating JSON parsing failure
- **Empty file**: Treat as invalid JSON and display appropriate message

### Validation Errors
- **Missing required properties**: Collect all missing properties and display them together
- **Multiple validation failures**: Display all validation errors in a clear, organized format

### Exit Codes
- **0**: Validation successful
- **1**: Validation failed (missing required properties)
- **2**: File system error (file not found, permission denied)
- **3**: JSON parsing error (invalid JSON syntax)

## Testing Strategy

### Unit Tests
- **File Reader**: Test file existence checks, file reading, error handling
- **JSON Parser**: Test valid JSON parsing, invalid JSON handling, edge cases
- **Validator**: Test all validation rules, error message generation
- **Output Formatter**: Test success and failure message formatting

### Integration Tests
- **End-to-end CLI**: Test complete validation flow with various devcontainer.json files
- **Error scenarios**: Test all error paths and exit codes
- **Edge cases**: Test with empty files, malformed JSON, missing files

### Test Data
- Valid devcontainer.json files with required properties
- Invalid files missing name property
- Invalid files missing image property
- Invalid files missing both properties
- Files with invalid JSON syntax
- Non-existent files for error testing

## Implementation Notes

### Technology Stack
- **Runtime**: Node.js (version 18+)
- **Language**: TypeScript for type safety
- **CLI Framework**: Native Node.js (no external CLI framework needed for simplicity)
- **Testing**: Jest for unit and integration tests
- **Build**: TypeScript compiler with npm scripts

### Performance Considerations
- Synchronous file reading is acceptable for CLI tool simplicity
- JSON parsing is handled by native JSON.parse for performance
- Minimal dependencies to keep the tool lightweight

### Extensibility
- Validation rules are modular and can be easily extended
- New validation rules can be added to the Validator class
- Output formatting can be enhanced without affecting core logic