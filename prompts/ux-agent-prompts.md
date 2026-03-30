# UX Designer Agent — Starter Prompts

**Who uses this:** UI/UX Designer
**When to activate:** Phase 2 (Planning)
**Command:** `bmad-create-ux-design`

---

## Starter Prompt: Create a UX Spec from PRD

```
I need to create a UX specification for our User Authentication System.

Here's the approved PRD: @samples/01-prd-user-auth.md

Our design system:
- Component library: Custom React components (similar to Shadcn/UI)
- Design tokens: 8px grid, Inter font family, blue primary (#2563EB)
- Responsive: Mobile-first, breakpoints at 640px, 768px, 1024px
- Accessibility: WCAG 2.1 AA minimum

Pages/flows I need designed:
1. Registration page
2. Login page
3. Forgot password flow (request → email → reset form)
4. OAuth login buttons (Google, GitHub)
5. Account disabled error state

For each page/flow, generate:
- Layout description with component hierarchy
- User interaction flow (what happens when they click, type, submit)
- Form validation rules and error message copy
- Loading states and success/error feedback
- Responsive behavior (mobile vs. desktop)
- Accessibility requirements (focus order, ARIA labels, screen reader behavior)
```

---

## Starter Prompt: Define Error States and Edge Cases

```
I need to define all user-facing error states for the authentication flow.

The PM's acceptance criteria say:
- Invalid login: show "Invalid email or password" (no info leakage)
- Account locked (5 failed attempts): show lockout message with time remaining
- Account disabled: show "Account disabled. Contact support."
- Password reset: show "If an account exists, we've sent a reset link" (no info leakage)

For each error state, help me define:
- Exact copy (what the user reads)
- Visual treatment (inline error, toast, full-page, modal?)
- Placement on the page
- Icon and color (following our error/warning/info pattern)
- Recovery action (what can the user do next?)
- Accessibility: how is this announced to screen readers?

I want these to be specific enough that a developer or AI agent
can implement them without guessing the design intent.
```

---

## Starter Prompt: Component Contracts for Dev Handoff

```
I need to create component contracts that the Developer Agent can use
to generate frontend code matching our design system.

For the Login page, define the following components:

1. LoginForm
   - Props/inputs
   - States (empty, filled, loading, error, success)
   - Validation rules
   - Submit behavior

2. OAuthButtonGroup
   - Which providers to show (Google, GitHub)
   - Button styling (outline, icon + text)
   - Loading state during OAuth redirect

3. ErrorBanner
   - Variants (inline field error, form-level error, account locked)
   - Auto-dismiss behavior (yes/no, after how many seconds?)
   - Animation (slide in, fade, none)

For each component, output:
- Props interface (TypeScript-style)
- Visual states with descriptions
- Interaction behavior
- Accessibility requirements
- Example usage

This becomes the contract between design and development — the AI agent
must generate components that match these contracts exactly.
```

---

## Starter Prompt: Validate Design Against Accessibility Standards

```
Review the following login page design for WCAG 2.1 AA compliance:

Page structure:
- Logo at top center
- Email input field with floating label
- Password input field with floating label + show/hide toggle
- "Forgot password?" link below password field
- "Log in" primary button (full width)
- Divider with "or continue with" text
- Google and GitHub OAuth buttons side by side
- "Don't have an account? Sign up" link at bottom

Check for:
- Color contrast ratios (our primary blue #2563EB on white)
- Focus order and keyboard navigation
- Form label associations
- Error announcement for screen readers
- Touch target sizes for mobile (minimum 44x44px)
- Reduced motion considerations
- Right-to-left (RTL) language support considerations

Flag issues as: MUST FIX (AA violation) / SHOULD FIX (best practice) / NICE TO HAVE
```

---

*Back to [Agents & Workflows Reference](../bmad-agents-and-workflows.md)*
