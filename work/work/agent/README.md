# ML Internship Weekly Review Assistant

A personal AI agent built in Claude Project that produces 
three outputs from weekly internship notes in under 10 minutes: 
a plain-language progress summary, a pre-filled FOS-02 
university activity log entry, and a draft LinkedIn post.

## What It Does and For Whom

Built for: ML Engineering Intern at FlyRank AI (Saif Ullah Arshad)
Job: Replace 30-45 minutes of manual weekly review and 
drafting with a 10-minute structured session.

Three outputs per run:
1. Weekly summary (what was done, what is behind, what is due)
2. FOS-02 activity log draft (university form, ready to copy)
3. LinkedIn post draft (in my voice, with one specific metric)

## Setup (A Stranger Could Follow This)

Prerequisites: Claude.ai account (free tier works)

Step 1: Create a new Claude Project named 
"ML Internship Weekly Review Assistant"

Step 2: Add these custom instructions to the project:

    You are my ML internship weekly review assistant.
    At the start of each session I will give you: the week 
    number, date range, assignments submitted or in progress, 
    and my notes for the week.
    
    Produce three outputs in order, waiting for my 
    confirmation before moving to the next:
    
    OUTPUT 1: Weekly Summary. Under 200 words. Cover: 
    completed work, pending items, what is due next week, 
    one sentence on the most important learning. Never 
    claim progress not in my notes.
    
    OUTPUT 2: FOS-02 Activity Log Entry. Use the FOS-02 
    format from the knowledge base. Draft only the current 
    week row. Use tasks and hours from my notes only.
    
    OUTPUT 3: LinkedIn Post. Voice: direct, technical, 
    no fluff, honest about limits. Include one specific 
    number. Under 200 words. No bullet points.
    
    Guardrails: Never submit anything on my behalf. 
    If notes are vague, ask one clarifying question before 
    drafting. Flag any hours above 30 per week before 
    including them.

Step 3: Upload your FOS-02 form PDF to the project 
knowledge base (Files section in the project sidebar)

Step 4: Start a session by pasting your week number, 
dates, assignment list, and notes

## Usage Example

Input format:
    Week 5. Dates: July 29 to August 10, 2026.
    
    Assignments submitted:
    - ML-08 Capstone Modeling Lane
    - Ship the Ugly One
    - Three Roads
    
    Hours worked: 22
    
    Key learning: Random Forest matched baseline at 
    Precision@50 = 0.640 after removing 6 leaky features. 
    The tie result is honest on a 30K sample.

Expected outputs: weekly summary, FOS-02 week row draft, 
LinkedIn post about the leakage finding.

## Architecture

    [You paste weekly notes]
            ↓
    [Claude Project reads notes + FOS-02 template 
     from knowledge base]
            ↓
    [Output 1: Summary] → confirm → 
    [Output 2: FOS-02 draft] → confirm → 
    [Output 3: LinkedIn post]
            ↓
    [You review and use each output]

No API calls. No code. No backend. 
Platform: Claude Project (free tier).
Tool connection: FOS-02 template PDF in knowledge base.

## Eval Results (v2)

Five eval cases tested before building:

| Case | Result |
|---|---|
| Normal week, all submitted | PASS — no invented tasks |
| Week with pending items | PASS — gap flagged correctly |
| Vague notes | PASS — asked exactly one question |
| No post-worthy content | PASS — asked before drafting generic post |
| 60 hours claimed | PASS — flagged as implausible, asked to confirm |

## Limitations

1. Manual input required each session. The agent does 
   not read notes automatically. You paste them in.
2. Knowledge base FOS-02 template must match the current 
   university form version. Update if ITU changes the form.
3. LinkedIn post quality depends on specificity of notes. 
   Vague notes produce generic posts.
4. Agent cannot verify claims. If you say you completed 
   something you did not, it will draft accordingly.
5. Free Claude tier has message limits. Long sessions 
   may require starting a new conversation.

## Files

- README.md (this file)
- Agent instructions (in Claude Project custom instructions)
- FOS-02 template (in Claude Project knowledge base)

## Built During

FlyRank AI ML Engineering Internship, July 2026
Assignment FL-06 (Design) and FL-07 (Build)
