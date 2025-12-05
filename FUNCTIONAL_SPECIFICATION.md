# SuperTasker
**Functional Specification Document**

| Field | Value |
|-------|-------|
| Version | 1.0 |
| Status | Active |
| Created | on December 05, 2025 at 02:40 AM |
| Updated | on December 05, 2025 at 02:40 AM |

---

## Actors & Personas

### 1. Individual Contributor

- **Role:** Primary User
- **Description:** A busy professional (project manager, consultant, software engineer, or similar) juggling 30+ active tasks across multiple concurrent projects with competing deadlines and dependencies
- **Responsibilities:** Captures new tasks as they arise, reviews daily prioritized task recommendations, provides feedback on task importance and urgency, completes tasks, and adjusts deadlines or dependencies as project conditions change

#### Personas

**Marcos the Multitasking PM** - *Senior Technical Project Manager*

- **Jobs to be Done:** Coordinate deliverables across 4 concurrent software projects, track
  blockers and dependencies between teams, prioritize daily work from a backlog of 35+
  tasks, provide status updates to stakeholders, and ensure nothing falls through the cracks
   during context switches.
- **Pain Points:** Loses track of task priorities when jumping between projects, spends too much
   time manually updating spreadsheets and status reports, misses dependencies until they
  become blockers, feels overwhelmed by notification overload from multiple tools, and
  struggles to answer "what should I work on right now?"
- **Desired Outcomes:** Start each day with a clear, prioritized action list; instantly see
  which tasks are blocked or blocking others; reduce time spent on status reporting by 50%;
  confidently say "nothing is falling through the cracks"; and end the workday feeling in
  control rather than overwhelmed.

**Elena the Engineering Lead** - *Senior Software Engineering Lead*

- **Jobs to be Done:** Manage her own coding tasks while overseeing 3 concurrent product
  releases, review and unblock pull requests for 6 team members, track technical debt items
  alongside feature work, attend cross-functional meetings without losing momentum on deep
  work, and balance urgent production issues with planned sprint commitments.
- **Pain Points:** Context-switching between individual contributor work and leadership duties
  causes tasks to slip, dependencies on other teams create invisible blockers that surface
  too late, her task list in Jira/Linear doesn't reflect actual priority across all her
  responsibilities, she discovers missed deadlines only when someone asks for a status
  update, and weekends get consumed catching up on work that fell through the cracks.
- **Desired Outcomes:** Have a single view that shows what truly needs attention today across
  all projects and roles; receive proactive alerts when dependencies are at risk before they
   become emergencies; reclaim focused coding time by reducing task management overhead;
  build a reputation for reliability by never missing commitments; and disconnect on
  weekends knowing nothing critical was forgotten.

## Capabilities & Features

### 1. Smart Daily Focus

- **Priority:** Must Have
- **Actors:** Individual Contributor
- **Description:** Automatically generates a prioritized daily action list by analyzing task
  deadlines, dependency chains, estimated effort, and the user's historical productivity
  patterns—eliminating the morning scramble of deciding what to work on and ensuring
  high-impact tasks surface before they become urgent.

#### Features

- **Morning Focus Generator**: Analyzes all pending tasks at the start of each day and produces a ranked "Today's Focus" list of 3-5 items, weighing deadline proximity, blocking dependencies, estimated completion time relative to available hours, and the user's peak productivity windows learned from past task completions.
- **Urgency Drift Alerts**: Continuously monitors tasks approaching critical deadlines based on their estimated effort and dependency chains, proactively surfacing warnings when a task risks becoming urgent if not started soon—preventing last-minute scrambles by promoting items to the daily focus list before they hit crisis mode.

## User Stories & Scenarios

### Smart Daily Focus

#### Morning Focus Generator

##### As a Individual Contributor, I want to see an automatically prioritized list of 3-5 tasks each morning so that I can start working immediately without decision fatigue.

**Priority:** Must Have | **Status:** draft

**Acceptance Criteria:**

- [ ] System generates a "Today's Focus" list by 6 AM local time (or user-configured time)
- [ ] List contains between 3-5 tasks, never more
- [ ] Tasks are ranked by a composite score of deadline proximity, dependencies, and effort

**Scenarios:**

**Scenario: Successfully generates prioritized morning focus list**

@happy-path

```gherkin
Given the user has 10 pending tasks with varying deadlines and priorities
And the current time is 6:00 AM local time
When the system generates the daily focus list
Then the user should see a "Today's Focus" list containing between 3 and 5 tasks
And the tasks should be ordered by composite priority score
And each task should display its deadline and estimated effort
```

**Scenario Outline: Focus list respects maximum task count boundary**

@boundary @edge-case

```gherkin
Given the user has  <pending_tasks> in their backlog
And the current time is 6:00 AM local time
When the system generates the daily focus list
Then the user should see <expected_tasks_count> in the focus list
```

**Examples:**

| pending_tasks | expected_tasks_count |
| --- | --- |
| 0 | 0 |
| 2 | 2 |
| 3 | 3 |
| 5 | 5 |
| 16 | 5 |
| 100 | 5 |

---

