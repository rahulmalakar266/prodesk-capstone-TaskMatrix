# Prompts.md – AI architectural queries

Tool used: Claude. Each entry lists the prompt, what I learned and the decision it led to.
(Replace or extend with your own real prompts as you work. Evaluators read this for prompt-engineering quality.)

## 1. Choosing the RFP
**Prompt:** "I'm on the Fullstack track and must pick one of: LMS, EHR dashboard, or Jira clone. Compare them on scope risk for 4 build weeks, number of MongoDB collections, and demo impact. Recommend one with reasons."
**Outcome:** TaskMatrix has the clearest MVP (board + tasks) and a natural real-time feature, with low domain complexity.

## 2. Scoping the MVP
**Prompt:** "Act as a product manager. Split these 14 features into P0/P1/P2 for a 4-sprint build by one developer. Flag anything that risks scope creep."
**Outcome:** Real-time feed moved to P1; AI and payments pushed out of MVP; video/file features cut.

## 3. Schema design
**Prompt:** "Design a MongoDB schema for a Kanban app with projects, members with roles, tasks, comments and an activity log. For each relation say embed vs reference and justify. Keep it to 5 collections."
**Outcome:** Embedded `members` in projects; separate `tasks`, `comments`, `activities`.

## 4. Drag-and-drop ordering
**Prompt:** "How should I store card order inside a Kanban column so that reordering is one write? Compare integer index, fractional index and linked list."
**Outcome:** Use a numeric `position` with midpoint insertion (fractional) and occasional rebalance.

## 5. RBAC
**Prompt:** "Show an Express middleware pattern for project-level roles (admin/member/viewer) where the role is read from the project's members array, not from the JWT."
**Outcome:** `requireRole('member')` middleware loads project membership per request.

## 6. Real time
**Prompt:** "Explain Socket.io rooms for per-project broadcasting and how to authenticate the socket with the same JWT."
**Outcome:** Room `project:{id}`; verify token in the connection handshake.

## 7. Deadline cron job
**Prompt:** "Design a node-cron job that runs daily, finds tasks past dueDate not done, and notifies the assignee once. How do I avoid duplicate notifications?"
**Outcome:** Added `overdueNotified` flag to `tasks`.

## 8. Wireframe review
**Prompt:** "Here is my screen list for a Kanban app. Which states am I missing (empty, loading, error, permission denied)? Suggest mobile adaptations for a 4-column board."
**Outcome:** Added viewer read-only state and a tabbed single-column mobile board.

## 9. Knowledge gaps for Sprint 15
**Prompt:** "List the 5 things most likely to block a first-time builder of drag-and-drop + Socket.io + JWT refresh in Next.js, with the doc pages to read."
**Outcome:** Reading list created for the planning week.
