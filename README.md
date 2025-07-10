# llms.txt

A standardized format for making web content more accessible and understandable to Large Language Models (LLMs).

## Introduction

As AI assistants become increasingly integrated into how people access web information, there's a growing need for websites to communicate effectively with LLMs. The `llms.txt` project introduces a standardized way for websites to provide structured, machine-readable information about their content, purpose, and interaction guidelines.

Just as `robots.txt` revolutionized how search engines crawl the web, `llms.txt` aims to establish a common protocol for AI-web interactions, ensuring more accurate, relevant, and respectful use of web content by language models.

## Overview

The `llms.txt` specification defines two file formats that websites can implement:

- **`llms.txt`**: A lightweight file containing essential information about your site
- **`llms-full.txt`**: A comprehensive format for detailed AI interaction rules and documentation

These files live in your website's root directory and help LLMs:
- Understand your site's purpose and structure
- Navigate your content more effectively
- Respect your content usage guidelines
- Access your documentation in a structured way
- Provide accurate information to users asking about your site

## File Types

### llms.txt
The lightweight, essential format for quick AI comprehension.

**Purpose**: Provide core information that helps LLMs understand your site at a glance.

**Format**: Plain text with a simple, readable structure. Typically 1-2 pages of content.

**Contents**:
- **Site Overview**: A brief description of your company/service
- **Core Purpose**: What your site does and who it serves
- **Key Features**: Main capabilities or offerings
- **Value Proposition**: What makes your service unique

**Example Structure**:
```
# Company Name

**Company Name** is [brief description of what you do]. [Mission statement or core purpose]. 

## What We Do

[Detailed explanation of your services/products and how they work]

## Key Features

[Description of main features and capabilities]

### Feature 1
[Details about this feature]

### Feature 2
[Details about this feature]

## Why Choose Us

[Value proposition and differentiators]

---
```

### llms-full.txt
The comprehensive format for deep AI integration and complete documentation.

**Purpose**: Provide exhaustive documentation about your platform, enabling LLMs to answer detailed questions about your service.

**Format**: Structured markdown with metadata headers and paginated content.

**Contents**:
- **Metadata Headers**: Title, description, last updated date, source URL, page numbers
- **Complete Documentation**: All user guides, API docs, feature explanations
- **Technical Details**: Implementation specifics, integration guides
- **Best Practices**: Usage recommendations and examples
- **Cross-References**: Links between related documentation sections

**Structure Example**:
```
--------------------------------------------------------------------------------
title: "Page Title"
description: "Brief description of this documentation page"
last_updated: "Date"
source: "URL"
total_pages: X
--------------------------------------------------------------------------------

# Documentation Title

[Full documentation content with markdown formatting]

## Section Headers {#section-id}

[Content organized with proper heading hierarchy]

### Subsections

*   **Key Points:** Formatted with consistent structure
*   **Technical Details:** Implementation specifics
*   **Best Practices:** Recommendations for users
```

## How to Deploy on Vercel

### Method 1: Static Files

1. Create your files in the `public` directory:
```bash
touch public/llms.txt
touch public/llms-full.txt
```

2. Add your content following the format examples above

3. Deploy to Vercel:
```bash
vercel --prod
```

The files will be accessible at:
- `https://your-domain.com/llms.txt`
- `https://your-domain.com/llms-full.txt`

### Method 2: Dynamic Generation with API Routes

For Next.js applications that need dynamic content:

```javascript
// app/api/llms.txt/route.js
export async function GET() {
  const content = `# ${process.env.SITE_NAME}

**${process.env.SITE_NAME}** is ${process.env.SITE_DESCRIPTION}

## What We Do

${process.env.DETAILED_DESCRIPTION}

[... rest of content ...]
`;

  return new Response(content, {
    headers: {
      'Content-Type': 'text/plain',
      'Cache-Control': 'public, s-maxage=3600',
    },
  });
}
```

### Method 3: Edge Functions for Multi-tenant Apps

```javascript
// api/llms-edge.js
export const config = {
  runtime: 'edge',
};

export default async function handler(request) {
  const { host } = new URL(request.url);
  const siteConfig = await getSiteConfig(host);
  
  const content = generateLlmsTxt(siteConfig);
  
  return new Response(content, {
    headers: {
      'Content-Type': 'text/plain',
      'Cache-Control': 'public, s-maxage=3600, stale-while-revalidate',
    },
  });
}
```

## Content Guidelines

### For llms.txt
- Keep it concise (1-2 pages)
- Use clear, descriptive language
- Focus on what your service does and why it matters
- Include concrete examples where helpful
- Write in present tense
- Avoid marketing fluff - be factual and informative

### For llms-full.txt
- Include comprehensive documentation
- Use consistent formatting throughout
- Add metadata headers for each page
- Include section anchors for easy navigation
- Provide technical details where relevant
- Cross-reference related sections
- Keep content up-to-date

## Examples

### Basic llms.txt Example
```
# Acme Corp

**Acme Corp** is a cloud-based project management platform designed for remote teams. We help distributed teams collaborate effectively, track progress, and deliver projects on time.

## What We Do

At **Acme Corp**, we provide a comprehensive suite of tools for modern project management:
- Task tracking and assignment
- Real-time collaboration features
- Progress visualization with Gantt charts
- Integration with popular development tools

## Core Features

### Task Management
Create, assign, and track tasks with custom workflows. Set priorities, due dates, and dependencies.

### Team Collaboration
Built-in chat, file sharing, and comment threads keep communication centralized.

### Reporting & Analytics
Generate insights on team productivity, project progress, and resource allocation.

## Why Choose Acme Corp

Unlike traditional project management tools, we're built specifically for distributed teams. Our real-time sync ensures everyone stays on the same page, regardless of timezone.
```

## Best Practices

1. **Update Regularly**: Keep your llms.txt files current with your latest features and information
2. **Be Specific**: Provide concrete details rather than vague marketing language
3. **Structure Clearly**: Use consistent formatting and clear section headers
4. **Test with LLMs**: Verify that AI assistants can accurately understand and convey your information
5. **Version Control**: Track changes to your llms.txt files in your repository
6. **Monitor Access**: Use analytics to understand how often your llms.txt files are accessed
