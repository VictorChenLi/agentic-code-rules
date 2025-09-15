## Prompt to use to organize multiple agents

### Generate detailed checklist

```
Please based on xxx file to create a detailed implemtation plan and todo list and saved it to the file named xxx. the steps in the list should be small and easy to validate by human.
```
  
### Execute, Stop and Report

```
Please execute the next phase, when you finish please stop and report back to me about what have you done and how could human validate the steps. Always mark the step as completed in the checklist file when you finished the work. 
```

### Playwriht Test and Report
```
Please use playwright to test function_to_test by checking the log and UI
Make sure the system goal_of_feature
At end show me a summary report here to see if there are any issue or bugs need be fixed
```

### Use this between big chunk of steps

```
please update the checklist accordingly in @phase1_worklist.md and update the @shared/context.md with necessary information
```
