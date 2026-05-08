---
name: browser-e2e-verification
description: Verifies browser workflows with realistic end-to-end, visual, accessibility, and interaction checks. Use when UI behavior matters, when adding frontend features, or when agent-generated code needs browser proof.
---

# Browser E2E Verification

## Overview

Browser verification proves that the product works where users experience it. Use this skill when unit or integration tests are insufficient because layout, navigation, auth, network behavior, accessibility, or browser state matters.

## When to Use

- Building or changing frontend workflows
- Verifying agent-generated UI code
- Reproducing browser-only bugs
- Adding regression coverage for user journeys
- Checking accessibility or visual behavior
- Proving that API and UI integration works together

## Workflow

### 1. Define The Journey

Write the user journey in plain language:

```markdown
Journey: Invite a teammate
1. Admin signs in.
2. Admin opens organization settings.
3. Admin enters an email address.
4. System sends invite and shows pending member.
```

### 2. Identify State And Data

Name the required fixtures:

- User roles
- Tenant or organization
- Existing records
- Empty states
- External services to mock or intercept

### 3. Test Critical Assertions

Assert behavior users can observe:

- Page or component appears
- Form validation blocks invalid input
- Network request succeeds or fails as expected
- Result persists after reload
- Unauthorized user is blocked
- Error state is recoverable

### 4. Add Visual And Accessibility Checks

For high-value UI:

- Check mobile and desktop viewports
- Check keyboard navigation
- Check focus states
- Check accessible names and roles
- Capture screenshot on failure
- Avoid fragile pixel-perfect assertions unless visual regression tooling is configured

## Playwright Pattern

```typescript
test('admin can invite a teammate', async ({ page }) => {
  await signInAs(page, 'admin');
  await page.goto('/settings/members');

  await page.getByRole('button', { name: 'Invite member' }).click();
  await page.getByLabel('Email').fill('new.member@example.com');
  await page.getByRole('button', { name: 'Send invite' }).click();

  await expect(page.getByText('Pending invitation')).toBeVisible();
  await expect(page.getByText('new.member@example.com')).toBeVisible();
});
```

## Anti-Flake Rules

- Prefer role and label selectors over CSS selectors
- Wait for meaningful UI state, not arbitrary timeouts
- Keep test data isolated
- Avoid depending on test execution order
- Mock only external boundaries, not the product behavior under test
- Capture traces for failed CI runs

## Verification

- [ ] Journey reflects a real user path
- [ ] Assertions prove visible behavior
- [ ] Negative and permission paths are covered where relevant
- [ ] Test data is isolated and deterministic
- [ ] Failures produce traces, screenshots, or useful logs
