 Claude Code Agent Communication SystemMultiple AIs collaborate to work, like a company-like development system What is this?In 3 lines explanation:Multiple AI agents (President, Manager, Workers) collaborate to develop
Each operates in different terminal screens and exchanges messages
Divides roles like a human organization to efficiently advance development

Actual achievements:Completed survey system (EmotiFlow) in 3 hours
Generated 12 innovative ideas
100% test coverage

 Try running it in 5 minutes!RequirementsMac or Linux
tmux (terminal splitting tool)
Claude Code CLI

Steps Download (30 seconds)bash

git clone https://github.com/nishimoto265/Claude-Code-Communication.git
cd Claude-Code-Communication

 Environment setup (1 minute)bash

./setup.sh

This prepares 5 terminal screens in the background! Open President screen and start AI (2 minutes)Open President screen:bash

tmux attach-session -t president

Start Claude in President screen:bash

# Browser authentication required
claude --dangerously-skip-permissions

 Start subordinates all at once (1 minute)Open a new terminal:bash

# Start 4 subordinates all at once
for i in {0..3}; do 
  tmux send-keys -t multiagent.$i 'claude --dangerously-skip-permissions' C-m
done

 Check subordinates' screens・Browser authentication for Claude may be required on each screenbash

tmux attach-session -t multiagent

This displays a 4-split screen:

┌────────┬────────┐
│ boss1  │worker1 │
├────────┼────────┤
│worker2 │worker3 │
└────────┴────────┘

 Enter the magic words (30 seconds)Then input:

You are president. Create a stylish and comprehensive IT company homepage.

Then automatically:President instructs Manager
Manager assigns work to 3 workers
Everyone collaborates to develop
Reports to President when completed

 Characters (Agents) President (PRESIDENT)Role: Determines overall policy
Features: Genius at understanding user's real needs
Catchphrase: "Please realize this vision"

 Manager (boss1)Role: Middle management that unites the team
Features: Master at drawing out members' creativity
Catchphrase: "Please provide 3 or more innovative ideas"

 Workers (worker1, 2, 3)worker1: Design担当 (UI/UX)
worker2: Data processing担当
worker3: Test担当

 How to communicate?How to send messagesbash

./agent-send.sh [recipient's name] "[message]"

# Example: Send to Manager
./agent-send.sh boss1 "This is a new project"

# Example: Send to worker1
./agent-send.sh worker1 "Please create the UI"

Actual interaction examplePresident → Manager:

You are boss1.

[Project Name] Survey System Development

[Vision]
A system that anyone can use easily, with results visible immediately

[Success Criteria]
- Complete response in 3 clicks
- Real-time result display

Please realize with innovative ideas.

Manager → Worker:

You are worker1.

[Project] Survey System

[Challenge]
Please propose 3 or more innovative ideas for UI design.

[Format]
1. Idea Name: [Catchy name]
   Overview: [Explanation]
   Innovation: [What is new]

 Important file explanationsInstructions (instructions/)Manuals for each agent's actionspresident.md - President's instructionmarkdown

# Your Role
As the best executive, understand the user's needs,
and show the vision

# 5 Layers of Needs Analysis
1. Surface: What to make
2. Functional: What it can do  
3. Benefits: What improves
4. Emotional: How they want to feel
5. Value: Why it's important

boss.md - Manager's instructionmarkdown

# Your Role
As a genius facilitator,
maximize the team's creativity

# 10 Minute Rule
Check progress every 10 minutes,
support struggling members

worker.md - Worker's instructionmarkdown

# Your Role
Utilize expertise to implement innovative solutions

# Task Management
1. Create to-do list
2. Execute in order
3. Report when complete

CLAUDE.mdSystem overall configuration filemarkdown

# Agent Communication System

## Agent Configuration
- PRESIDENT: Overall responsible
- boss1: Team leader  
- worker1,2,3: Execution responsible

## Message Sending
./agent-send.sh [recipient] "[message]"

 What was actually created: EmotiFlowWhat was made? Survey where emotions can be expressed with emojis
 Results visible in real-time
 Usable on smartphones too

Try itbash

cd emotiflow-mvp
python -m http.server 8000
# Open http://localhost:8000 in browser

File structure

emotiflow-mvp/
├── index.html    # Main screen
├── styles.css    # Design
├── script.js     # Operation logic
└── tests/        # Tests

 TroubleshootingQ: Agent doesn't respondbash

# Check status
tmux ls

# Restart
./setup.sh

Q: Message doesn't arrivebash

# View log
cat logs/send_log.txt

# Manual test
./agent-send.sh boss1 "Test"

Q: Want to start over from the beginningbash

# Reset all
tmux kill-server
rm -rf ./tmp/*
./setup.sh

 Create your own projectSimple example: Make a TODO appInput in President (PRESIDENT):

You are president.
Please make a TODO app.
Simple and easy to use, with task addition, deletion, and completion.

Then automatically:Manager breaks down tasks
worker1 creates UI
worker2 manages data
worker3 creates tests
Complete!

 System mechanism (illustration)Screen configuration

┌─────────────────┐
│   PRESIDENT     │ ← President's screen (purple)
└─────────────────┘

┌────────┬────────┐
│ boss1  │worker1 │ ← Manager (red) and worker1 (blue)
├────────┼────────┤
│worker2 │worker3 │ ← worker2 and 3 (blue)
└────────┴────────┘

Communication flow

President
 ↓ "Realize the vision"
Manager
 ↓ "Everyone, come up with ideas"
Workers
 ↓ "Done!"
Manager
 ↓ "All complete"
President

Progress management mechanism

./tmp/
├── worker1_done.txt     # File created when worker1 completes
├── worker2_done.txt     # File created when worker2 completes
├── worker3_done.txt     # File created when worker3 completes
└── worker*_progress.log # Progress records

 Why is this amazing?Conventional development

Human → AI → Result

This system

Human → AI President → AI Manager → AI Workers ×3 → Integration → Result

Advantages:3 times faster with parallel processing
Utilizes expertise
Abundant ideas
High quality

 For those who want to know moreHow to write promptsGood example:

You are boss1.

[Project Name] Clear name
[Vision] Specific ideal
[Success Criteria] Measurable indicators

Bad example:

Make something

Customization methodsAdd new worker:Create instructions/worker4.md
Edit setup.sh to add pane
Add mapping to agent-send.sh

Change timer:bash

# In instructions/boss.md
sleep 600  # Change 10 minutes to 5 minutes
sleep 300

 SummaryThis system, with multiple AIs collaborating:Completes a full-fledged web app in 3 hours
Generates 12 innovative ideas
Achieves 100% test coverage

Please try it and experience the power of an AI team!Author: GitHub
License: MIT
Questions: Please go to Issues!Reference Links・Claude Code Official
　　URL: https://docs.anthropic.com/ja/docs/claude-code/overview   ・Tmux Cheat Sheet & Quick Reference | Session, window, pane and more
　　URL: https://tmuxcheatsheet.com/   ・Akira-Papa/Claude-Code-Communication
　　URL: https://github.com/Akira-Papa/Claude-Code-Communication   ・【tmuxでClaude CodeのMaxプランでAI組織を動かし放題のローカル環境ができた〜〜〜！ので、やり方をシェア！！】 #AIエージェント - Qiita
　　URL: https://qiita.com/akira_papa_AI/items/9f6c6605e925a88b9ac5   ・Claude Code コマンドチートシート完全ガイド #ClaudeCode - Qiita
　　URL: https://qiita.com/akira_papa_AI/items/d68782fbf03ffd9b2f43   ※The following information was referenced to build this tmux Claude Code organization environment. Thank you so much!    ◇Mr. Motoki, the originator who made it possible to build Claude Code bidirectional communication with shell in one hit
Reference GitHub ：
haconiwa/README_JA.md at main · dai-motoki/haconiwa
　　URL: https://github.com/dai-motoki/haconiwa/blob/main/README_JA.md   ・KAMUI（@kamui_qai
） / X
　　URL: https://x.com/kamui_qai
   ◇Daikon-san who shared how to easily build Claude Code bidirectional communication environment
Reference GitHub：
nishimoto265/Claude-Code-Communication
　　URL: https://github.com/nishimoto265/Claude-Code-Communication   ・ Daikon（@daikon265
） / X
　　URL: https://x.com/daikon265
   ◇Claude Code official explanation video:
Mastering Claude Code in 30 minutes - YouTube
　　URL: https://www.youtube.com/live/6eBSHbLKuN0?t=1356s

