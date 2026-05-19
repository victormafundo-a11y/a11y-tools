# Getting Started with a11y-tools

Welcome to a11y-tools! This guide will help you set up and start using the tools.

## Installation

### Using npm

```bash
npm install a11y-tools
```

### Using yarn

```bash
yarn add a11y-tools
```

## Quick Start

### 1. Basic Setup

```typescript
import { AccessibilityChecker } from 'a11y-tools';

const checker = new AccessibilityChecker({
  standard: 'WCAG2AA'
});
```

### 2. Check a URL

```typescript
const results = await checker.checkUrl('https://example.com');
console.log(results);
```

### 3. Check HTML

```typescript
const html = `
  <button>Click me</button>
`;

const results = await checker.checkHtml(html);
```

## Configuration

### Standard Options

- `WCAG2A` - Level A compliance
- `WCAG2AA` - Level AA compliance (recommended)
- `WCAG2AAA` - Level AAA compliance (strict)
- `Section508` - US Federal accessibility requirements

### Example

```typescript
const checker = new AccessibilityChecker({
  standard: 'WCAG2AA',
  ignoreWarnings: false,
  timeout: 30000
});
```

## Understanding Results

Each check returns a `CheckResult` object:

```typescript
interface CheckResult {
  status: 'pass' | 'fail' | 'warning';
  issues: Issue[];
  timestamp: Date;
  standard: string;
}
```

### Interpreting Issues

```typescript
results.issues.forEach(issue => {
  console.log(`${issue.severity}: ${issue.message}`);
  console.log(`Location: Line ${issue.line}, Column ${issue.column}`);
});
```

## Common Use Cases

### Continuous Integration

Check accessibility in your CI/CD pipeline:

```typescript
import { AccessibilityChecker } from 'a11y-tools';

async function validateAccessibility() {
  const checker = new AccessibilityChecker({
    standard: 'WCAG2AA'
  });
  
  const results = await checker.checkUrl(process.env.APP_URL);
  
  if (results.status === 'fail') {
    process.exit(1);
  }
}
```

### Testing

Use in your test suite:

```typescript
describe('Accessibility', () => {
  it('should pass WCAG2AA', async () => {
    const results = await checker.checkHtml(component.html());
    expect(results.status).toBe('pass');
  });
});
```

## Best Practices

1. **Test Early and Often** - Run checks during development
2. **Start with AA** - WCAG 2.1 AA is the industry standard
3. **Fix Errors First** - Address errors before warnings
4. **Use Multiple Tools** - Combine with manual testing
5. **Document Issues** - Track and document accessibility fixes

## Troubleshooting

### Issue: "Cannot find module 'a11y-tools'"

Make sure you've installed the package:
```bash
npm install a11y-tools
```

### Issue: Timeout errors

Increase the timeout:
```typescript
const checker = new AccessibilityChecker({
  standard: 'WCAG2AA',
  timeout: 60000
});
```

## Next Steps

- Read the [API Reference](./api-reference.md)
- Learn about [WCAG Guidelines](./wcag-guidelines.md)
- Check out [Best Practices](./best-practices.md)

## Need Help?

- [Open an issue](https://github.com/victormafundo-a11y/a11y-tools/issues)
- [Visit our wiki](https://github.com/victormafundo-a11y/a11y-tools/wiki)
- [Start a discussion](https://github.com/victormafundo-a11y/a11y-tools/discussions)
