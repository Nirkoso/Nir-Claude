# Lovable.dev Prompting Best Practices

**A comprehensive guide to writing effective prompts for AI-powered web development with Lovable.dev**

*Last Updated: December 2025*

---

## Overview

Lovable.dev is a full-stack AI application development platform that generates production-ready, editable source code from natural language prompts. Unlike traditional no-code builders that create visual blocks, Lovable produces real code using modern frameworks like React, TypeScript, Tailwind CSS, and shadcn/ui components, with backend support through Supabase integration.

The platform enables developers, designers, and entrepreneurs to build complete web applications 20x faster than traditional coding methods through conversational prompting. With Lovable 2.0 released in mid-2025, the platform has introduced enhanced Chat Mode, better version control, and improved collaboration features.

**Why Prompting Matters:** The quality of your prompts directly determines the quality of your output. Effective prompting can mean the difference between a polished, production-ready application and hours of debugging and refinement.

---

## 1. Understanding Lovable.dev

### Platform Capabilities

**Full-Stack Development:**
- Frontend: React, TypeScript, Vite, Tailwind CSS, shadcn/ui components
- Backend: Supabase integration (PostgreSQL, authentication, edge functions)
- Authentication: Email/password, OAuth, JWT handling
- Database: Automatic schema generation from prompts
- API Integration: OpenAPI backends, external API connections
- Deployment: GitHub sync, export to Vercel/Netlify

**Core Features:**
- Natural language to production code conversion
- Real-time collaboration (Teams plan)
- GitHub integration with bi-directional sync
- Version control with pinning and revert capabilities
- Chat Mode for planning and debugging
- Visual preview with responsive testing
- Code export and full ownership

### Ideal Use Cases

Lovable.dev excels at:
- Rapid prototyping and MVP development
- Landing pages and marketing sites
- SaaS applications with authentication
- Internal tools and dashboards
- Form-based applications
- CRUD applications with database backends
- Portfolio and showcase websites
- Content management systems

### Limitations

- Complex enterprise-grade applications may require developer refinement
- Advanced backend logic better handled in specialized environments
- Some basic coding knowledge helpful for customization
- Supabase revert limitations (database schema doesn't revert cleanly)
- Best suited for web applications (not mobile native apps)

### Target Users

- Solo entrepreneurs turning ideas into businesses
- Product designers going from idea to prototype
- Sales teams building interactive product demos
- Developers rapidly prototyping features
- Non-technical founders building MVPs
- Agencies delivering client projects faster

---

## 2. Prompt Structure Fundamentals

### The Golden Rule

**Be clear, specific, and incremental.** Treat Lovable's AI like an engineering partner who only knows what you tell them.

### Best Practice Format

Use this structured approach for complex features:

```
PROJECT CONTEXT:
[Brief description of what you're building]

CURRENT STATE:
[What exists now in your app]

DESIRED OUTCOME:
[What you want to achieve with this prompt]

SPECIFIC REQUIREMENTS:
- [Requirement 1]
- [Requirement 2]
- [Requirement 3]

TECHNICAL DETAILS:
- [Framework preferences, styling notes, etc.]

QUESTIONS:
Ask me any questions you need to fully understand what I want from this feature and how I envision it.
```

### Starting a New Project

**Initial Prompt Template:**

```
I want to build [TYPE OF APP] that helps [TARGET USER] to [MAIN PURPOSE].

Key features:
1. [Feature 1]
2. [Feature 2]
3. [Feature 3]

Design style: [minimal/modern/playful/premium/etc.]

Tech requirements:
- Supabase for backend
- User authentication required
- Mobile-first responsive design

Always make things responsive on all breakpoints, with a focus on mobile first. Use modern UI/UX best practices for determining how breakpoints should change the components. Use shadcn and tailwind built-in breakpoints.

Ask me any questions you need to fully understand my vision before starting.
```

### Incremental Prompting Strategy

**The most effective approach:** Break work into small, testable chunks.

**Example workflow:**

1. **First prompt:** "Create the landing page hero section with headline, subheadline, and CTA button"
2. **Second prompt:** "Add a features section with 3 feature cards below the hero"
3. **Third prompt:** "Implement the navigation bar with logo and menu items"
4. **Fourth prompt:** "Connect the CTA button to open a signup modal"

This incremental approach:
- Produces better results than massive prompts
- Makes debugging easier (errors caught early)
- Allows testing after each step
- Maintains better control over implementation

---

## 3. Specificity & Detail Guidelines

### When to Be Specific

**High Specificity Needed:**
- Authentication flows and user roles
- Database schema and relationships
- API endpoints and data structures
- Security requirements and RLS policies
- Error handling behavior
- Form validation rules
- Exact UI component placement

**Example:**
```
❌ Bad: "Add a login page"
✅ Good: "Create a login page at /login with email/password fields, a 'Remember me' checkbox, a 'Forgot password?' link, and implement JWT-based authentication using Supabase. Show error messages in red below each field. Redirect to /dashboard on successful login."
```

### When to Be General

**Let AI Make Decisions:**
- Visual styling details (unless specific brand required)
- Layout spacing and padding
- Animation timing and easing
- Component internal structure
- Color harmony within a palette

**Example:**
```
✅ Good: "Create a modern, minimal landing page with a premium feel. Use soft shadows, generous spacing, and a clean color palette."
```

### Use Style Buzzwords

Lovable understands design terminology that influences typography, spacing, shadows, borders, and color:

- **Minimal:** Clean, sparse, ample whitespace
- **Expressive:** Bold typography, vibrant colors
- **Cinematic:** Dramatic contrast, layered depth
- **Playful:** Rounded corners, bright colors, fun interactions
- **Premium:** Luxury feel, subtle elegance, refined details
- **Developer-focused:** Terminal aesthetics, monospace fonts, dark themes

### Atomic Vocabulary

Be precise in naming UI elements:

❌ Vague: "a user interface"
✅ Specific: "a modal with a success toast notification after submit"

❌ Vague: "add some cards"
✅ Specific: "add three horizontally-aligned feature cards with icons, headings, and descriptions"

---

## 4. UI/UX Prompting

### Describing Layouts

**Effective layout descriptions:**

```
Create a dashboard with:
- Sidebar navigation on the left (fixed, 240px wide)
- Top navigation bar with user profile dropdown on the right
- Main content area with a 3-column grid of metric cards
- Below the cards, add a full-width data table with pagination
- Make sidebar collapsible on tablet and below
```

### Mobile-First Approach

**Essential mobile prompt:**

```
Always make things responsive on all breakpoints, with a focus on mobile first. Use modern UI/UX best practices for determining how breakpoints should change components. Use shadcn and tailwind built-in breakpoints instead of anything custom, unless I prompt for custom breakpoints directly.
```

### Responsive Design Patterns

Describe how layout should adapt:

```
Desktop (1024px+): Show 4 cards per row
Tablet (768px-1023px): Show 2 cards per row
Mobile (below 768px): Stack cards vertically, full width
```

### Design Systems & Consistency

**Establishing a design system:**

```
Create a consistent design system with:
- Primary color: #3B82F6 (blue)
- Secondary color: #10B981 (green)
- Typography: Inter for headings, system fonts for body
- Border radius: 8px for cards, 4px for buttons
- Spacing scale: 4px base unit (4, 8, 16, 24, 32, 48, 64)
- Shadows: soft, subtle elevation
- Use shadcn/ui components throughout for consistency
```

Add this to your Knowledge Base for consistency across all prompts.

### Image-Based Prompting

Lovable supports screenshots and images:

```
[Upload screenshot]
"Create and implement a UI that looks as similar as possible to the attached image. Match the layout, spacing, colors, and component hierarchy."
```

```
[Upload error screenshot]
"This screenshot shows a layout issue on mobile. Adjust margins and padding to make it responsive while keeping the same design structure."
```

### Animations & Interactions

```
Add smooth hover effects to all buttons (scale 1.05, 200ms ease)
Fade in the hero section on page load
Add a loading skeleton while data fetches
Show a success toast notification after form submission that auto-dismisses after 3 seconds
```

---

## 5. Functionality & Features

### User Interactions

Be explicit about what happens when users interact:

```
When the user clicks the "Export" button:
1. Show a loading spinner on the button
2. Fetch data from the /api/export endpoint
3. Download the file as "report.csv"
4. Show a success message
5. Reset the button state
```

### State Management

Describe data flow and state:

```
Create a task list where:
- Tasks are stored in Supabase 'tasks' table
- Each task has: id, title, completed (boolean), created_at
- Display tasks in reverse chronological order
- Users can toggle completion with a checkbox
- Update the database immediately on toggle
- Show optimistic UI updates before server confirmation
```

### Forms & Validation

```
Create a signup form with:
- Email field (validate email format)
- Password field (minimum 8 characters, require 1 number, 1 special char)
- Confirm password field (must match password)
- Show real-time validation errors below each field
- Disable submit button until all fields are valid
- Show loading state during submission
- Display server errors if registration fails
```

### API Integration

**Connecting external APIs:**

```
Integrate the OpenWeather API:
1. Add an API key input field in settings
2. Create a function to fetch weather data for a given city
3. Display: temperature, description, icon, humidity
4. Handle loading states and error cases (city not found, API error)
5. Cache results for 10 minutes to avoid excessive API calls
```

### Authentication Flows

```
Set up Supabase authentication with:
- Email/password signup and login pages
- Email verification required before access
- Password reset flow via email link
- Protected routes that redirect to /login if not authenticated
- Store user profile data in 'profiles' table
- Implement RLS policies so users only see their own data
```

---

## 6. Iterative Development

### The Incremental Workflow

**Phase 1: Foundation**
```
Prompt 1: "Create the basic layout with navigation and footer"
Prompt 2: "Add the hero section with headline and CTA"
Prompt 3: "Set up Supabase and create the users table"
```

**Phase 2: Core Features**
```
Prompt 4: "Implement user signup with email/password"
Prompt 5: "Add login page and authentication flow"
Prompt 6: "Create the main dashboard page for logged-in users"
```

**Phase 3: Refinement**
```
Prompt 7: "Add loading states to all forms"
Prompt 8: "Improve mobile responsiveness on the dashboard"
Prompt 9: "Add error handling for failed API calls"
```

### Building on Previous Work

Reference existing components:

```
"Using the same card style from the features section, create a testimonials section with 3 testimonial cards"

"Apply the same hover effect from the CTA button to all secondary buttons"

"Use the existing modal component to create a settings dialog"
```

### Refining Existing Code

```
"The hero section looks good, but:
- Increase the headline font size by 20%
- Add more vertical padding (64px top and bottom)
- Make the CTA button more prominent with a subtle glow effect"
```

### Testing & Validation

Build in testing as you go:

```
"After implementing the signup form, test that:
- Form validation works correctly
- Error messages display properly
- Successful signup redirects to dashboard
- Duplicate email shows appropriate error"
```

---

## 7. Using Lovable's Key Features

### Knowledge Base

**What to include:**

The Knowledge Base gets sent with every prompt, so include:

```
PROJECT OVERVIEW:
- App name: TaskFlow
- Purpose: Team task management for small businesses
- Target users: Teams of 5-20 people

DESIGN SYSTEM:
- Primary: #3B82F6
- Secondary: #10B981
- Fonts: Inter for all text
- Border radius: 8px
- Consistent shadcn/ui components

USER ROLES:
- Admin: Full access, can manage users
- Member: Can view and edit own tasks
- Guest: View-only access

TECHNICAL STANDARDS:
- Always use Supabase for data
- Implement RLS policies on all tables
- Mobile-first responsive design
- Show loading states on all async operations
- Handle all error cases with user-friendly messages

CODING CONVENTIONS:
- Use TypeScript strict mode
- Prefer functional components
- Extract components when files exceed 200 lines
- Use descriptive variable names
- Add comments for complex logic
```

**Best practice:** Review and update your Knowledge Base after each major milestone.

### Chat Mode vs. Implement

**Chat Mode** (60-70% of development time):
- Planning features before implementation
- Debugging and analyzing errors
- Asking questions and clarifying requirements
- Reviewing code changes
- Getting AI to outline a plan

**Example Chat Mode usage:**
```
"Don't implement yet. First, outline your plan for adding multi-user collaboration to this task list. Consider database schema, real-time updates, permissions, and UI changes."
```

Only click **"Implement the plan"** when fully satisfied with the approach.

### Versioning & Pinning

**Best practices:**

1. **Pin after every working feature**
   - Marks stable states you can return to
   - Makes it easy to revert when experiments fail

2. **Use descriptive labels**
   - "✅ Working signup flow"
   - "✅ Dashboard with data display"
   - "✅ Pre-deployment stable"

3. **Revert thoughtfully**
   - Try "Try to Fix" up to 3 times first
   - Revert to last pinned version if stuck
   - Note: Supabase database doesn't revert cleanly

4. **Visual comparison**
   - Preview versions before reverting
   - Compare UI changes side-by-side

### GitHub Integration

**Set up early:**

1. Settings → Integrations → GitHub
2. Connect and authorize
3. Automatic bi-directional sync
4. Every Lovable edit becomes a commit
5. Changes in GitHub sync back to Lovable

**Benefits:**
- Full code ownership
- Standard Git workflow
- Deploy to Vercel, Netlify, or custom hosting
- Collaborate with developers outside Lovable
- Production-ready code export

---

## 8. Do's and Don'ts

### Planning & Strategy

| DO | DON'T |
|---|---|
| ✅ Plan your app structure before starting | ❌ Jump in without clear user flows |
| ✅ Write down features, workflows, and goals | ❌ Make up requirements as you go |
| ✅ Use the Knowledge Base for project context | ❌ Repeat the same context in every prompt |
| ✅ Start simple, add complexity incrementally | ❌ Try to build everything at once |
| ✅ Implement authentication first | ❌ Add authentication as an afterthought |

### Prompting

| DO | DON'T |
|---|---|
| ✅ Break tasks into small, focused prompts | ❌ Dump massive multi-feature prompts |
| ✅ Be specific about behavior and interactions | ❌ Use vague terms like "make it work" |
| ✅ Let AI ask clarifying questions | ❌ Assume AI understands ambiguous requests |
| ✅ Use atomic, precise vocabulary | ❌ Use general terms like "user interface" |
| ✅ Describe outcomes, not implementation | ❌ Tell AI exactly how to code something |
| ✅ Add screenshots for visual reference | ❌ Try to describe complex UIs in words only |

### Development Workflow

| DO | DON'T |
|---|---|
| ✅ Test after each increment | ❌ Build for hours without testing |
| ✅ Use Chat Mode to plan before implementing | ❌ Immediately implement without review |
| ✅ Pin versions after working features | ❌ Forget to mark stable states |
| ✅ Use "Try to Fix" button for errors | ❌ Manually debug AI-generated code first |
| ✅ Regularly refactor large components | ❌ Let files grow beyond 300 lines |
| ✅ Review AI's plan before clicking "Implement" | ❌ Auto-accept all AI suggestions |

### Database & Backend

| DO | DON'T |
|---|---|
| ✅ Use separate test environments | ❌ Test on live production data |
| ✅ Implement RLS policies from the start | ❌ Leave database security for later |
| ✅ Let Lovable generate schema from prompts | ❌ Manually create tables then ask for code |
| ✅ Describe data relationships clearly | ❌ Assume AI will infer complex relationships |

### Debugging

| DO | DON'T |
|---|---|
| ✅ Copy error messages into Chat Mode | ❌ Say "nothing works, fix it!" |
| ✅ Use "Try to Fix" up to 3 times | ❌ Keep retrying the same fix indefinitely |
| ✅ Revert to last working version if stuck | ❌ Dig deeper into broken state |
| ✅ Investigate errors before making changes | ❌ Make random changes hoping to fix issues |

### Styling & Design

| DO | DON'T |
|---|---|
| ✅ Use style buzzwords (minimal, premium, etc.) | ❌ Over-specify every pixel and color |
| ✅ Let AI handle spacing and harmony | ❌ Micromanage design details unnecessarily |
| ✅ Use shadcn/ui and Tailwind breakpoints | ❌ Request custom breakpoints unless needed |
| ✅ Focus on mobile-first responsive design | ❌ Build desktop-only and adapt later |

---

## 9. Advanced Techniques

### Chain of Thought Debugging

For complex errors, ask AI to reason through the problem:

```
"Use chain-of-thought reasoning to identify the root cause of why the form submission is failing. Think step by step through the data flow from form input to database."
```

### Context Building Across Sessions

Maintain context in long development sessions:

```
"Before we continue, review the Knowledge Base and summarize your understanding of:
1. The app's purpose
2. Current features implemented
3. Database schema
4. User roles and permissions"
```

### Referencing External Documentation

```
"Implement file upload using Supabase Storage. Reference the Supabase Storage documentation for best practices. Ask me for the bucket configuration details you need."
```

### Performance Optimization

```
"Analyze the dashboard page for performance bottlenecks:
- Identify unnecessary re-renders
- Optimize database queries (show me the query plans)
- Implement pagination for the task list
- Add loading skeletons for better perceived performance"
```

### Accessibility Requirements

```
"Ensure the entire app meets WCAG 2.1 AA standards:
- Proper heading hierarchy
- Alt text for all images
- Keyboard navigation support
- Sufficient color contrast (check all text)
- ARIA labels where needed
- Focus indicators on interactive elements"
```

### Multi-Step Features with Dependencies

```
"We'll implement a commenting system in phases. First, outline the complete plan including database schema, UI components, and real-time updates. Wait for my approval before implementation."

[After reviewing the plan]

"Great plan! Let's proceed:
Phase 1: Create the database schema for comments
[Wait for completion]
Phase 2: Build the UI for displaying comments
[Wait for completion]
Phase 3: Add the comment input form and submission
[Wait for completion]
Phase 4: Implement real-time updates using Supabase subscriptions"
```

### Design Patterns & Architecture

```
"Implement a reusable data fetching pattern:
- Create a custom hook `useDataFetch` that handles loading, error, and success states
- Include retry logic for failed requests
- Add request deduplication
- Cache results for 5 minutes
- Show me the hook implementation first before using it throughout the app"
```

### Collaborative Prompting (Teams)

When working in teams, maintain clarity:

```
"Team context: Sarah built the authentication system (pinned version from 12/1). I'm adding the dashboard. Use the same design tokens and component patterns Sarah established. Do not modify auth-related files."
```

---

## 10. Common Pitfalls & Solutions

### Pitfall 1: The AI Loop

**Problem:** AI keeps breaking things while trying to fix them.

**Solutions:**
- Stop after 3 "Try to Fix" attempts
- Revert to last pinned working version
- Use Chat Mode to analyze root cause
- Simplify your request and try incrementally

### Pitfall 2: Vague Results

**Problem:** Output doesn't match your vision.

**Solutions:**
- Add screenshots or mockups
- Use specific style buzzwords
- Break down the request into smaller pieces
- Add more detail to Knowledge Base
- Let AI ask clarifying questions

### Pitfall 3: Database Schema Issues

**Problem:** Database structure becomes messy or breaks.

**Solutions:**
- Plan schema before implementing
- Use Chat Mode to review schema design
- Be explicit about relationships and foreign keys
- Remember: Database doesn't revert cleanly with version control
- Test schema changes in a separate Supabase project first

### Pitfall 4: Large Messy Files

**Problem:** Components become too large and confusing.

**Solutions:**
- Regularly refactor files over 200 lines
- Extract reusable components
- Prompt: "This component is getting large. Split it into smaller sub-components for better maintainability"

### Pitfall 5: Authentication Added Late

**Problem:** Adding auth later disrupts entire app structure.

**Solutions:**
- Always implement authentication first
- Build other features assuming authenticated users
- Set up RLS policies from the beginning
- Test with both authenticated and unauthenticated states

### Pitfall 6: Confusing Prompts

**Problem:** AI misunderstands or produces unexpected results.

**Solutions:**
- Use atomic, specific vocabulary
- Describe the outcome, not the implementation
- Provide context about what already exists
- Ask AI to confirm understanding before implementing

### Pitfall 7: Overwhelmed by Errors

**Problem:** Too many errors to handle at once.

**Solutions:**
- Don't tackle all errors simultaneously
- Fix one error at a time, test, then continue
- Use Chat Mode to prioritize errors
- Consider reverting if error count is too high

---

## 11. Example Prompts: Good vs. Bad

### Example 1: Login Page

**❌ Bad:**
```
"Build a login page"
```

**Why it's bad:** Too vague. No details about authentication method, styling, behavior, or error handling.

**✅ Good:**
```
"Create a login page at /login with:
- Email and password input fields
- 'Remember me' checkbox
- 'Forgot password?' link that navigates to /reset-password
- 'Sign up' link navigating to /signup
- Submit button that authenticates using Supabase
- Show validation errors in red below each field
- Show a loading spinner on the button during authentication
- Redirect to /dashboard on success
- Display server errors (invalid credentials, etc.) in a toast
- Use a minimal, modern design with the primary color from our design system
- Fully responsive on mobile"
```

### Example 2: Dashboard Component

**❌ Bad:**
```
"Make a dashboard with some charts"
```

**Why it's bad:** No specifics about layout, data source, chart types, or user interactions.

**✅ Good:**
```
"Create a dashboard page at /dashboard that displays:

LAYOUT:
- Top: Welcome message with user's name and current date
- Below: 3 metric cards in a row showing:
  * Total tasks (number)
  * Completed this week (number with percentage badge)
  * Overdue tasks (number, highlighted if > 0)
- Below metrics: Line chart showing task completion trend over last 30 days
- Bottom: Data table of recent tasks with columns: Title, Status, Due Date, Priority

DATA:
- Fetch all data from Supabase 'tasks' table
- Apply RLS policy (user sees only their tasks)
- Show loading skeletons while data loads

INTERACTIONS:
- Clicking a metric card filters the table below
- Table rows link to /tasks/[id] for details
- Refresh data every 60 seconds

RESPONSIVE:
- Desktop: 3 cards per row
- Tablet: 2 cards per row, chart below
- Mobile: Stack everything vertically"
```

### Example 3: Supabase Integration

**❌ Bad:**
```
"Connect Supabase"
```

**Why it's bad:** Doesn't specify what to connect, what data structure, or what features are needed.

**✅ Good:**
```
"Set up Supabase for this project management app:

DATABASE SCHEMA:
- Create 'projects' table with: id (uuid), name (text), description (text), owner_id (uuid, foreign key to auth.users), created_at (timestamp)
- Create 'tasks' table with: id (uuid), project_id (uuid, foreign key), title (text), description (text), status (enum: todo, in_progress, done), assignee_id (uuid, foreign key to auth.users), due_date (date), created_at (timestamp)

AUTHENTICATION:
- Enable email/password authentication
- Create a 'profiles' table linked to auth.users for storing user display names and avatars

RLS POLICIES:
- Projects: Users can only view/edit projects they own or are members of
- Tasks: Users can view all tasks in their projects, but only edit tasks assigned to them

Show me the SQL for the schema and RLS policies before implementing."
```

### Example 4: Styling Refinement

**❌ Bad:**
```
"Make it look better"
```

**Why it's bad:** Completely subjective with no actionable direction.

**✅ Good:**
```
"Refine the landing page hero section:
- Increase headline font size to 3.5rem (desktop) and 2.5rem (mobile)
- Add a subtle gradient overlay to the background image (dark at bottom)
- Increase vertical padding to 120px top and bottom
- Make the CTA button larger (16px→18px font, 14px→18px padding)
- Add a soft glow effect to the CTA button on hover
- Improve contrast between text and background (ensure WCAG AA compliance)
- Add a smooth fade-in animation when the page loads"
```

### Example 5: Debugging Request

**❌ Bad:**
```
"Nothing works, fix it!"
```

**Why it's bad:** Provides zero information about the problem.

**✅ Good:**
```
"The form submission is failing with this error in the console:
'Cannot read property 'id' of undefined'

Context:
- This happens when I click the 'Save' button on the project creation form
- The error appears in the handleSubmit function
- This started after we added the team member assignment feature

Can you:
1. Identify where the 'id' is being accessed incorrectly
2. Check if all required fields are being validated before submission
3. Fix the error and add proper error handling
4. Test that both creating new projects and editing existing projects work"
```

### Example 6: Feature Request with Context

**❌ Bad:**
```
"Add comments to the app"
```

**Why it's bad:** No context about where comments go, who can comment, or how they're structured.

**✅ Good:**
```
"Add a commenting system to task detail pages:

FEATURES:
- Comment section below task details
- Each comment shows: author name, avatar, timestamp, comment text
- 'Add comment' textarea with 'Post' button at bottom
- Comments sorted by newest first
- Real-time updates (if another user comments, it appears without refresh)

DATABASE:
- Create 'comments' table: id, task_id (foreign key), author_id (foreign key to auth.users), content (text), created_at
- RLS: Users can view comments on tasks they have access to, but only edit/delete their own comments

UI:
- Use the same avatar component from the user profile
- Style comments with subtle background cards
- Add smooth fade-in animation for new comments
- Show 'No comments yet' placeholder if empty

First, show me your plan for the implementation including the database schema and component structure. Don't implement until I approve."
```

---

## 12. Workflow Cheatsheet

### Starting a New Project

1. ✅ Write a project brief (save to Knowledge Base)
2. ✅ Define your design system (colors, fonts, style)
3. ✅ Plan your database schema
4. ✅ Create your first prompt with project context
5. ✅ Implement authentication first
6. ✅ Connect Supabase early
7. ✅ Connect to GitHub early

### During Development

1. ✅ Use Chat Mode 60-70% of the time
2. ✅ Break work into small increments
3. ✅ Test after each change
4. ✅ Pin versions after working features
5. ✅ Preview on mobile regularly
6. ✅ Let AI ask clarifying questions
7. ✅ Review plans before implementing

### When Things Break

1. ✅ Copy exact error message to Chat Mode
2. ✅ Try "Try to Fix" button (max 3 times)
3. ✅ Ask AI to analyze root cause with chain-of-thought
4. ✅ If stuck, revert to last pinned version
5. ✅ Simplify your request and rebuild incrementally

### Before Deployment

1. ✅ Test all user flows thoroughly
2. ✅ Check mobile responsiveness on all pages
3. ✅ Verify authentication and permissions work
4. ✅ Test error states and edge cases
5. ✅ Review database RLS policies
6. ✅ Pin a "pre-deployment" stable version
7. ✅ Push final code to GitHub
8. ✅ Deploy via Vercel, Netlify, or your host

---

## 13. Quick Reference

### Prompt Structure Template

```
CONTEXT: [What exists now]
GOAL: [What you want to achieve]
REQUIREMENTS:
- [Specific requirement 1]
- [Specific requirement 2]
TECHNICAL: [Framework/styling notes]
QUESTIONS: Ask me any questions needed for clarity.
```

### Essential Prompts to Include

**Mobile-first standard:**
```
Always make things responsive on all breakpoints, with a focus on mobile first. Use modern UI/UX best practices and shadcn/Tailwind breakpoints.
```

**Let AI ask questions:**
```
Ask me any questions you need to fully understand what I want from this feature and how I envision it.
```

**Request a plan first:**
```
Don't implement yet. First, outline your plan for [feature] including [technical considerations]. Wait for my approval.
```

**Chain-of-thought debugging:**
```
Use chain-of-thought reasoning to identify the root cause of [problem]. Think step by step.
```

### Style Buzzwords

- **Minimal** - Clean, sparse, whitespace
- **Premium** - Luxury, refined, subtle
- **Cinematic** - Dramatic, layered depth
- **Playful** - Rounded, bright, fun
- **Expressive** - Bold typography, vibrant
- **Developer-focused** - Terminal aesthetic, dark

### Key Features to Remember

| Feature | Use Case |
|---|---|
| **Knowledge Base** | Store project context, design system, standards |
| **Chat Mode** | Plan, debug, ask questions before implementing |
| **Pinning** | Mark stable versions to revert to |
| **Try to Fix** | Quick error resolution (try 3x max) |
| **GitHub Sync** | Code ownership, version control, deployment |
| **Supabase Integration** | Backend, database, auth, edge functions |

### When to Use Chat vs. Implement

| Use Chat Mode | Use Implement |
|---|---|
| Planning new features | When plan is approved and clear |
| Analyzing errors | After Chat Mode confirms approach |
| Reviewing code changes | For straightforward, small changes |
| Getting AI to explain | When you've tested the plan |
| Brainstorming approaches | N/A |

---

## 14. Real-World Case Studies

### Case Study 1: Dummy Forms by Tomas

**Project:** Form builder and management tool
**Builder:** Tomas (15+ years coding experience)
**Timeline:** Part of 10 apps built rapidly
**Status:** Active production

**Approach:**
- Used incremental prompting for each feature
- Leveraged Supabase for backend
- Built mobile-first responsive design
- Iterated based on user feedback

**Key Success Factors:**
- Broke complex form builder into small components
- Tested each form element type individually
- Used Knowledge Base for consistent design patterns

### Case Study 2: TrackMyInfluencer.com

**Project:** Marketing tool for influencer campaign tracking
**Builder:** Tomas
**Status:** Production

**Features Built:**
- Influencer management dashboard
- Campaign ROI tracking
- Data visualization charts
- Team collaboration features

**Prompting Strategy:**
- Started with authentication and user roles
- Built dashboard incrementally (metrics → charts → tables)
- Added integrations one at a time
- Refined UI based on real usage

### Case Study 3: Landing Page + Agency Form

**Project:** Agency website with submission form
**Timeline:** Under 28 minutes
**Tech:** Lovable + Supabase integration

**Process:**
1. Created landing page structure (5 min)
2. Added hero section and features (8 min)
3. Built contact form (6 min)
4. Integrated Supabase backend (5 min)
5. Tested and refined (4 min)

**Key Insight:** Incremental approach with clear, specific prompts enabled rapid development.

### Case Study 4: 3D Interactive Environment

**Project:** Physics-based 3D space with interactive objects
**Builder:** Konstantin (Developer Advocate)
**Challenge:** Complex 3D graphics and physics

**Approach:**
1. Started simple: "Create a 3D space with floating objects"
2. Added features iteratively: grid lines, lighting, shadows
3. Implemented physics: collision detection, gravity simulation
4. Added interactions: click, drag, rotate objects
5. Refined performance: optimized rendering

**Lesson:** Even complex features can be built incrementally with clear prompts.

### Case Study 5: Full-Stack Habit Tracker

**Timeline:** 5 hours
**Features:**
- User authentication
- Daily habit tracking
- Streak calculations
- Progress visualization
- Mobile-responsive design

**Workflow:**
- Hour 1: Auth setup and basic layout
- Hour 2: Database schema and habit CRUD
- Hour 3: Tracking interface and daily view
- Hour 4: Streak calculations and progress charts
- Hour 5: Mobile optimization and testing

**Success Factors:**
- Clear database schema from the start
- Tested each feature before moving forward
- Used pinning after each working hour

---

## 15. Common Questions & Answers

**Q: How long should my prompts be?**
A: Focus on clarity over length. A well-structured 5-line prompt beats a rambling 20-line prompt. For complex features, 10-15 lines with clear structure is ideal.

**Q: Should I write code myself or let Lovable handle everything?**
A: Let Lovable generate the code. If you need customization, export to GitHub and edit locally, or give Lovable specific prompts about the changes.

**Q: How do I handle features Lovable struggles with?**
A: Break them into smaller pieces. If still struggling, build in Lovable what it does well (UI, CRUD operations) and integrate with external services for complex logic.

**Q: Can I use Lovable for production apps?**
A: Yes. The code is production-ready, exportable, and fully yours. Many apps built with Lovable are in active production serving real users.

**Q: What if I don't like the design AI generates?**
A: Either provide more specific design requirements upfront, upload reference images, or incrementally refine: "Make the buttons larger", "Use more whitespace", "Change color to #3B82F6".

**Q: How do I maintain consistency across my app?**
A: Use the Knowledge Base to define your design system (colors, fonts, spacing, components). Reference existing components: "Use the same card style as the features section."

**Q: When should I revert vs. keep fixing?**
A: If "Try to Fix" doesn't work after 3 attempts, or if you're unsure what broke, revert to your last pinned version and rebuild incrementally.

**Q: Can multiple people work on the same Lovable project?**
A: Yes, with a Teams plan. Use GitHub integration for additional collaboration with developers outside Lovable.

---

## 16. Resources & Community

### Official Documentation

- **Main Docs:** https://docs.lovable.dev
- **Prompting Guide:** https://docs.lovable.dev/prompting/prompting-one
- **The Lovable Prompting Bible:** https://lovable.dev/blog/2025-01-16-lovable-prompting-handbook
- **Prompt Engineering Tips:** https://docs.lovable.dev/tips-tricks/prompting
- **Best Practices:** https://docs.lovable.dev/tips-tricks/best-practice
- **Troubleshooting:** https://docs.lovable.dev/tips-tricks/troubleshooting

### Integrations

- **Supabase Integration:** https://docs.lovable.dev/integrations/supabase
- **GitHub Integration:** https://docs.lovable.dev/integrations/github
- **Knowledge Base:** https://docs.lovable.dev/features/knowledge

### Community & Support

- **Discord Community:** https://discord.com/invite/lovable-dev
- **Support:** https://lovable.dev/support
- **Feedback Portal:** https://feedback.lovable.dev
- **Hall of Fame:** https://lovable.dev/hall-of-fame

### Learning Resources

- **Video Tutorials:** https://lovable.dev/videos
- **Supabase Tutorials:** https://lovable.dev/videos/supabase
- **How-To Guides:** https://lovable.dev/how-to

### Third-Party Guides

- **UI Bakery - What is Lovable AI:** https://uibakery.io/blog/what-is-lovable-ai
- **Designer's Prompting Guide:** https://christiangrech.medium.com/how-to-10x-your-ui-with-lovable-a-designers-prompting-guide-5e1a610c3838
- **Lovable + Cursor Integration:** https://lovable.dev/video/transfer-lovabledev-projects-to-cursor-ai-via-github-integration
- **OpenReplay - Do's and Don'ts:** https://blog.openreplay.com/do-and-dont-of-using-lovable-dev/

### Tools & Extensions

- **Lovable Prompt Creator:** https://lovableprompts.app
- **shadcn/ui Components:** https://ui.shadcn.com
- **Tailwind CSS Docs:** https://tailwindcss.com/docs

---

## 17. Sources

This guide was compiled from the following sources:

### Official Lovable Documentation
- [Lovable Documentation](https://docs.lovable.dev)
- [Prompt Better in Lovable](https://docs.lovable.dev/prompting/prompting-one)
- [The Lovable Prompting Bible](https://lovable.dev/blog/2025-01-16-lovable-prompting-handbook)
- [Prompt Engineering](https://docs.lovable.dev/tips-tricks/prompting)
- [Best Practices](https://docs.lovable.dev/tips-tricks/best-practice)
- [Troubleshooting](https://docs.lovable.dev/tips-tricks/troubleshooting)
- [Custom Knowledge](https://docs.lovable.dev/features/knowledge)
- [Supabase Integration](https://docs.lovable.dev/integrations/supabase)
- [GitHub Integration](https://docs.lovable.dev/integrations/github)
- [Versioning 2.0 Announcement](https://lovable.dev/blog/versioning-with-lovable-two-point-zero)
- [Better Version Management](https://lovable.dev/blog/2025-01-13-better-version-management-and-speed-enhancements)

### Platform Reviews & Analysis
- [What is Lovable AI? - UI Bakery](https://uibakery.io/blog/what-is-lovable-ai)
- [Lovable AI Review - Trickle](https://trickle.so/blog/lovable-ai-review)
- [Lovable.dev Review - Refine](https://refine.dev/blog/lovable-ai/)
- [Lovable.dev: The AI Coding Platform - ITMunch](https://itmunch.com/lovable-dev-ai-coding-platform-2025/)
- [Lovable AI Complete Guide - Prismetric](https://www.prismetric.com/what-is-lovable-ai/)

### Community Guides & Tutorials
- [The Lovable Prompting Bible - Rapid Dev](https://www.rapidevelopers.com/blog/the-lovable-prompting-bible-complete-guide-to-ai-prompting-in-lovable-2025)
- [How I Built a Working App with AI in 12 Prompts](https://slobodskyi.com/create/no-code/lovable)
- [How to 10x Your UI with Lovable - Christian Grech](https://christiangrech.medium.com/how-to-10x-your-ui-with-lovable-a-designers-prompting-guide-5e1a610c3838)
- [Mastering the Prompt - Analyse Digital](https://analysedigital.com/mastering-the-prompt-how-to-get-the-best-results-from-lovable/)
- [Designer's Prompting Guide - Medium](https://medium.com/design-bootcamp/how-to-10x-your-ui-with-lovable-b38a668cfdd2)

### Best Practices & Pitfalls
- [Do's and Don'ts of Using Lovable.dev - OpenReplay](https://blog.openreplay.com/do-and-dont-of-using-lovable-dev/)
- [5 Essential Tips for Building Full-Stack Apps](https://blog.openreplay.com/tips-for-building-full-stack-apps-with-lovable/)
- [Why Lovable Projects Keep Breaking](https://momen.app/blogs/why-lovable-projects-keep-breaking-and-how-to-fix-them/)
- [Vibe Coding Mistakes Killing Your Projects](https://lumberjack.so/vibe-coding-mistakes-lovable-projects/)
- [Why Most Projects Built on Lovable.dev Fail](https://www.nextrocket.io/blog/why-most-projects-built-on-lovable-dev-fail-and-how-you-can-avoid-it)
- [The Guideline for a Successful Lovable Project](https://madewithlovable.com/resources/successful-project-lovable)

### Debugging & Development Workflow
- [Debugging AI-Generated Code with Lovable AI](https://www.sidetool.co/post/debugging-ai-generated-code-with-lovable-ai-essential-tips/)
- [Debugging Workflows with Lovable AI](https://lovableai.site/guides/prompting/debugging-workflows/)
- [Debugging Lovable Bugs - Jeff Clark](https://www.clarkle.com/notes/debugging-lovable-bugs/)

### Supabase & Backend Integration
- [How to Set Up Supabase Authentication](https://lovable.dev/blog/supabase-authentification-step-by-step)
- [Lovable Supabase Integration - UI Bakery](https://uibakery.io/blog/lovable-supabase-integration)
- [Lovable Tutorial: OpenAI and Supabase Integration](https://www.nocode.mba/articles/lovable-openai-supabase)

### UI/UX & Design
- [Lovable AI for UX - LogRocket](https://blog.logrocket.com/ux-design/lovable-ai-for-ux/)
- [Anyone Can Create An App - UX/UI/Dev With AI](https://lovable.dev/video/anyone-can-create-an-app-uxuidev-with-ai)
- [Frontend Development with Lovable](https://lovable.dev/blog/frontend-development-with-lovable)

### Deployment & Export
- [How to Export Lovable.dev Code to GitHub](https://vibecodingwithfred.com/blog/export-lovable-to-github-complete/)
- [Host Lovable.dev Project on GitHub Pages](https://dev.to/coderatul/host-lovabledev-project-on-github-pages-1c61)
- [Publish Your Lovable App to InMotion Hosting](https://www.inmotionhosting.com/support/website/git/publish-lovable-webapp-via-github/)
- [Build with Lovable and Deploy with DeployHQ](https://www.deployhq.com/guides/lovable)

### Case Studies
- [Case Studies: Successful Apps Built on Lovable.dev](https://blog.loveableapps.ai/case-studies-successful-apps-built-on-lovable-dev/)
- [How a Canadian Infanteer Built 10 Apps](https://lovable.dev/blog/2025-01-20-how-a-canadian-infanteer-built-10-apps-in-record-time-with-lovable-dev)
- [How a Developer Advocate Built 3D Projects](https://lovable.dev/blog/2025-01-20-how-a-developer-advocate-built-stunning-3d-projects-with-lovable-dev-and-won-big)
- [Lovable.dev's Rapid Success Story - Design Monks](https://www.designmonks.co/case-study/lovable-ai-app-builder)

### Version Control & Git
- [Managing Git and Version Control in Lovable](https://www.rapidevelopers.com/lovable-issues/managing-git-and-version-control-in-lovable-projects)
- [GitHub Integration Documentation](https://docs.lovable.dev/integrations/git-integration)

### Styling & Components
- [Why Designers Should Care About Tailwind and ShadCN](https://annaarteeva.medium.com/why-designers-should-care-about-tailwind-and-shadcn-especially-in-the-ai-era-55b744c42603)
- [shadcn/ui Documentation](https://ui.shadcn.com/)

---

**Document Version:** 1.0
**Last Updated:** December 4, 2025
**Maintained by:** Deep Research Agent

---

*This guide is a living document. As Lovable.dev evolves and new best practices emerge, this guide will be updated to reflect the latest recommendations and community insights.*
