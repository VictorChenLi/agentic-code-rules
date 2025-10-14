## Prompt to use to organize multiple agents

### Generate detailed checklist

```
Please based on xxx file to create a detailed implemtation plan and todo list and saved it to the file named xxx. the steps in the list should be small and easy to validate by human.
```
  
### Execute, Stop and Report (start new session for one feature at a time, unless the memory is less than 50%)

```
Read the _contextfiles_ and _planfile_ first, and please execute the next phase, when you finish please stop and report back to me about what have you done and how could human validate the steps. Always mark the step as completed in the checklist file when you finished the work. 
```

### Playwright Test and Report
```
Please use playwright to test the system by checking the log and UI
Make sure the system able to goal_of_feature
At end show me a summary report here to see if there are any issue or bugs need be fixed
```

### Chat Project Playwriht Test and Report
```
Please use Playwright to test the system by checking the log and UI, use the account in claude.md
Send at least 20 turns with nezha, check and make sure the system able to
1. compact the memory and summarize correctly
2. Tier A model able to move the plot forward after each compact
3. Tier B model response not repeating
At end show me a summary report here to see if there are any issue or bugs need be fixed
```

### Use this between big chunk of steps

```
please update the checklist accordingly in @phase1_worklist.md and update the @shared/context.md with necessary information
```
