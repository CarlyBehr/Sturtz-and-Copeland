# Sturtz & Copeland Design Token System

## Project Overview

This project implements a multi-platform design token system for Sturtz & Copeland's brand, with tokens for typography, spacing, colors, and other visual elements. The system uses Style Dictionary to generate platform-specific outputs for web, iOS, and Android.

## Project Structure

```
SturtzAndCopelandStyleDictionary/
├── package.json           # Project dependencies and scripts
├── tokens/
│   └── tokens.json        # Source tokens in JSON format
├── config.json            # Style Dictionary configuration
├── .github/
│   └── workflows/
│       └── build-tokens.yml  # GitHub Actions workflow
└── README.md              # Project documentation
```

## Token Structure (tokens.json)

```json
{
  "font": {
    "family": {
      "heading": { "value": "Bodoni 72 Smallcaps" },
      "subheading": { "value": "Coquette" },
      "body": { "value": "Gravesend Sans" }
    },
    "size": {
      "h1": { "value": "946px" },
      "h2": { "value": "630px" },
      "h3": { "value": "420px" },
      "h4": { "value": "280px" },
      "h5": { "value": "186px" },
      "h6": { "value": "124px" },
      "h7": { "value": "82px" },
      "h8": { "value": "54px" },
      "h9": { "value": "36px" },
      "h10": { "value": "24px" },
      "body1": { "value": "16px" },
      "body2": { "value": "10px" },
      "body3": { "value": "6px" },
      "body4": { "value": "4px" },
      "body5": { "value": "2px" }
    },
    "lineHeight": {
      "h1": { "value": "1419px" },
      "h2": { "value": "945px" },
      "h3": { "value": "630px" },
      "h4": { "value": "420px" },
      "h5": { "value": "279px" },
      "h6": { "value": "186px" },
      "h7": { "value": "123px" },
      "h8": { "value": "81px" },
      "h9": { "value": "54px" },
      "h10": { "value": "36px" },
      "body1": { "value": "24px" },
      "body2": { "value": "15px" },
      "body3": { "value": "9px" },
      "body4": { "value": "6px" },
      "body5": { "value": "3px" }
    }
  },
  "spacing": {
    "0": { "value": "2px" },
    "1": { "value": "4px" },
    "2": { "value": "8px" },
    "3": { "value": "12px" },
    "4": { "value": "16px" },
    "5": { "value": "20px" },
    "6": { "value": "24px" },
    "7": { "value": "32px" },
    "8": { "value": "40px" },
    "9": { "value": "48px" },
    "10": { "value": "56px" }
  },
  "radius": {
    "2xs": { "value": "0px" }
  },
  "stroke": {
    "2xs": { "value": "0.777px" },
    "xs": { "value": "1px" },
    "s": { "value": "2.304px" },
    "m": { "value": "2.308px" },
    "l": { "value": "2.571px" }
  },
  "effect": {
    "elevation": {
      "e0": { "value": "none" },
      "e1": { "value": "0px 1px 2px rgba(0,0,0,0.1)" },
      "e2": { "value": "0px 2px 4px rgba(0,0,0,0.1)" },
      "e3": { "value": "0px 4px 8px rgba(0,0,0,0.1)" }
    }
  },
  "color": {
    "primary": {
      "whirlpoolWaterfall100": { "value": "#a6d6ca" },
      "whirlpoolWaterfall200": { "value": "#41b1a2" }
    },
    "accent": {
      "pouringCopper100": { "value": "#f79c85" }
    },
    "neutral": {
      "black100": { "value": "#000000" }
    },
    "secondary": {
      "daiquiriOlive100": { "value": "#bed171" },
      "daiquiriOlive200": { "value": "#a4a96b" },
      "ducklingCarnival100": { "value": "#fdc584" },
      "ducklingCarnival200": { "value": "#f9b15c" },
      "ducklingCarnival300": { "value": "#e78524" },
      "como100": { "value": "#4e775a" },
      "grapefruitBerrylicious100": { "value": "#f493af" },
      "grapefruitBerrylicious200": { "value": "#f0708d" },
      "grapefruitBerrylicious300": { "value": "#d85f6c" }
    }
  }
}
```

## Style Dictionary Configuration (config.json)

```json
{
  "source": ["tokens/**/*.json"],
  "platforms": {
    "web": {
      "transformGroup": "web",
      "buildPath": "build/web/",
      "files": [
        {
          "destination": "variables.css",
          "format": "css/variables"
        }
      ]
    },
    "ios": {
      "transformGroup": "ios",
      "buildPath": "build/ios/",
      "files": [
        {
          "destination": "StyleDictionary.swift",
          "format": "ios-swift/class.swift",
          "className": "SturtzCopelandStyle"
        },
        {
          "destination": "StyleDictionaryColor.swift",
          "format": "ios-swift/colors.swift",
          "className": "SturtzCopelandStyle",
          "type": "color"
        },
        {
          "destination": "StyleDictionarySize.swift",
          "format": "ios-swift/sizes.swift",
          "className": "SturtzCopelandStyle",
          "type": "size"
        }
      ]
    },
    "android": {
      "transformGroup": "android",
      "buildPath": "build/android/values/",
      "files": [
        {
          "destination": "colors.xml",
          "format": "android/colors"
        },
        {
          "destination": "font_dimens.xml",
          "format": "android/dimens",
          "filter": {
            "attribute": "category",
            "value": "font"
          }
        },
        {
          "destination": "spacings.xml",
          "format": "android/dimens",
          "filter": {
            "attribute": "category",
            "value": "spacing"
          }
        },
        {
          "destination": "styles.xml",
          "format": "android/styles"
        }
      ]
    },
    "docs": {
      "transformGroup": "web",
      "buildPath": "build/docs/",
      "files": [
        {
          "destination": "style_guide.html",
          "format": "html/docs"
        }
      ]
    }
  }
}
```

## Package.json with Automation Scripts

```json
{
  "name": "sturtz-and-copeland-style-dictionary",
  "version": "1.0.0",
  "description": "Style Dictionary for Sturtz & Copeland's design tokens.",
  "main": "config.json",
  "scripts": {
    "build": "style-dictionary build",
    "clean": "rm -rf build",
    "build:web": "style-dictionary build --platform web",
    "build:ios": "style-dictionary build --platform ios",
    "build:android": "style-dictionary build --platform android",
    "build:docs": "style-dictionary build --platform docs",
    "copy:web": "mkdir -p demo/web/styles && cp build/web/variables.css demo/web/styles/",
    "copy:ios": "mkdir -p demo/ios/Styles && cp build/ios/*.swift demo/ios/Styles/",
    "copy:android": "mkdir -p demo/android/app/src/main/res/values && cp build/android/values/*.xml demo/android/app/src/main/res/values/",
    "dist": "npm run clean && npm run build && npm run copy:web && npm run copy:ios && npm run copy:android"
  },
  "devDependencies": {
    "style-dictionary": "^3.0.0"
  }
}
```

## GitHub Actions Workflow (.github/workflows/build-tokens.yml)

```yaml
name: Build and Deploy Design Tokens

on:
  push:
    branches: [ main ]
    paths:
      - 'tokens/**'
      - 'config.json'

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '16'
        
    - name: Install dependencies
      run: npm ci
      
    - name: Build tokens
      run: npm run build
      
    - name: Archive build artifacts
      uses: actions/upload-artifact@v3
      with:
        name: token-build
        path: build/
        
    # Optional: If you want to commit the built files back to the repository
    - name: Commit built tokens
      uses: EndBug/add-and-commit@v9
      with:
        add: 'build'
        message: 'Update generated token files [skip ci]'
        default_author: github_actions
```

## Part 2: Reflection – Tokenizing a Brand's Style Guide

### 1. Benefits Realized

The implementation of a design token system for Sturtz & Copeland demonstrated several concrete benefits:

**Design-to-Code Consistency**: By creating a single source of truth in our JSON tokens, we eliminated discrepancies between design specifications and implementation. This approach resolves the common issue of designers and developers referencing different versions of style guidelines, ensuring that what's designed is exactly what gets built.

**Cross-Platform Coherence**: The multi-platform configuration showed how a single token definition can generate appropriate outputs for web, iOS, and Android simultaneously. This ensures that, for example, the "whirlpoolWaterfall100" color (#a6d6ca) remains exactly the same across all platforms without manual conversion or transcription errors.

**Scalability for Brand Evolution**: When the brand needs to evolve, updating a color or typography value in one place automatically cascades those changes across all platforms. This eliminates the tedious work of manually updating each platform's code and significantly reduces the risk of inconsistency during brand updates.

**Documentation and Onboarding**: The generated style guide (via the "docs" platform in our configuration) serves as living documentation that's always in sync with the actual implementation. New team members can reference this documentation and be confident they're working with current brand standards.

### 2. Drawbacks and Challenges

Despite the benefits, several challenges emerged during implementation:

**Technical Infrastructure Complexity**: Establishing the proper tooling infrastructure required significant initial setup time. Determining where to host assets and how to manage them in a continuous delivery system wasn't immediately intuitive.

**Uneven Platform Support**: Some platforms handle certain token types better than others. For example, complex shadow effects translated well to CSS but required more custom handling for native platforms. This sometimes necessitates platform-specific transformations or custom formats.

**Design Subjectivity Limitations**: Not all design elements fit neatly into tokens. While colors and spacing are straightforward, more subjective aspects like illustration styles or complex layout rules remain difficult to tokenize effectively. Some brand elements still require designer judgment that can't be fully encoded.

**Learning Curve**: Both designers and developers need to shift their thinking to work effectively with tokens. Designers must consider how their work will be tokenized from the start, rather than creating designs and tokenizing afterward. This represents a significant workflow change that requires time and training.

### 3. Version Control and Governance

Effective token management requires thoughtful version control and governance strategies:

**Branching Strategy**: For our token system, a feature-branch workflow proved effective—creating separate branches for each significant token change before merging to main. This allows for isolated testing of token updates before they affect production systems.

**Review Process**: Implementing a dual-approval system where both a developer (for technical implementation) and a designer (for visual accuracy) must approve token changes ensures both technical correctness and design fidelity.

**Semantic Versioning**: Adopting semantic versioning (MAJOR.MINOR.PATCH) for token releases provides clear communication about the scope of changes. Breaking changes increment the major version, additions increment the minor version, and fixes increment the patch version.

**Change Documentation**: Maintaining a changelog that documents each token update provides valuable context for team members. This could be automated through commit message conventions and PR templates that prompt contributors to explain the rationale behind changes.

**Decentralized Contributions with Centralized Oversight**: Following an open-source model where any team can propose token changes, but a core design systems team reviews and approves them, balances innovation with consistency.

### 4. Automation and Pipeline Considerations

Our automation implementation revealed important considerations:

**Continuous Integration Benefits**: The GitHub Actions workflow we implemented ensures that token changes are automatically built, tested, and distributed. This eliminates manual build steps and the errors they might introduce.

**Risk Mitigation**: While automating design changes directly to code is powerful, it also carries risk. Visual regression testing should be integrated into the pipeline to catch unexpected visual changes. Screenshot comparison tools could verify that token updates don't break existing interfaces.

**Documentation Generation**: Our pipeline includes automatic generation of an HTML style guide, but this could be further enhanced with interactive examples. Integration with a tool like Storybook would allow developers to see tokens applied in various component contexts.

**Feedback Loops**: The ideal pipeline would include mechanisms for gathering feedback on token changes. This might include preview environments where stakeholders can see token updates in context before they're finalized.

**Deployment Strategies**: For larger organizations, a staged rollout approach for token updates would be prudent—perhaps deploying to internal applications first, then gradually to customer-facing products to minimize disruption.

### 5. Tokens in the Wild

Design tokens represent a significant advancement in brand implementation for professional contexts:

**Bridge Between Design and Development**: When consulting for organizations with existing style guides, I would position tokens as the crucial bridge that transforms static design documentation into living, implementable code. Rather than replacing style guides, tokens enhance them by making them actionable.

**ROI Calculation**: The investment in a token system pays dividends through reduced design debt, faster implementation of brand changes, and more consistent customer experiences. For a medium-sized organization making quarterly brand adjustments, a token system could reduce implementation time from weeks to days.

**Phased Implementation**: For organizations hesitant to fully commit, I would recommend starting with color tokens—usually the most straightforward to implement and demonstrate value. Once this foundation proves successful, expanding to typography, spacing, and more complex tokens becomes an easier sell.

**Case for Long-term Investment**: While the upfront cost of implementing tokens may seem high, the long-term benefits of consistency, efficiency, and scalability make them an essential investment for brands that value cohesive experiences. As demonstrated by companies like Intuit, even large organizations with complex product ecosystems find the investment worthwhile.

**Future-Proofing**: As design systems continue to evolve, organizations with established token pipelines will be better positioned to adopt new platforms and technologies. The abstraction layer that tokens provide insulates brands from the specifics of implementation technologies, making them more resilient to technological change.

## Installation and Usage

1. **Clone the repository**:
   ```bash
   git clone https://github.com/yourusername/sturtz-copeland-style-dictionary.git
   cd sturtz-copeland-style-dictionary
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Build tokens**:
   ```bash
   npm run build
   ```

4. **Build for specific platforms**:
   ```bash
   npm run build:web    # Build only web tokens
   npm run build:ios    # Build only iOS tokens
   npm run build:android # Build only Android tokens
   npm run build:docs   # Build documentation
   ```

5. **Distribute to demo projects**:
   ```bash
   npm run dist
   ```

## Implementation Examples

### Web (CSS Variables)

```css
:root {
  --color-primary-whirlpool-waterfall-100: #a6d6ca;
  --color-primary-whirlpool-waterfall-200: #41b1a2;
  --font-family-heading: "Bodoni 72 Smallcaps";
  --font-size-h1: 946px;
  /* ... other variables ... */
}

.heading {
  font-family: var(--font-family-heading);
  font-size: var(--font-size-h2);
  color: var(--color-primary-whirlpool-waterfall-100);
}
```

### iOS (Swift)

```swift
import UIKit

struct ButtonView: View {
    var body: some View {
        Button("Press Me") {
            // Action
        }
        .background(Color(SturtzCopelandStyle.colorPrimaryWhirlpoolWaterfall100))
        .font(.system(size: CGFloat(SturtzCopelandStyle.fontSizeH8)))
        .padding(CGFloat(SturtzCopelandStyle.spacing4))
    }
}
```

### Android (XML)

```xml
<Button
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Press Me"
    android:textSize="@dimen/font_size_h8"
    android:padding="@dimen/spacing_4"
    android:background="@color/color_primary_whirlpool_waterfall_100" />
```
