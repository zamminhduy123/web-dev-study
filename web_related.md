# Task Queue and Job Queue in Depth

Task Queue or Macro Task holds **Task** like setTimeout, setInterval, setImmediate, I/O tasks, etc.
Job Queue or Micro Task holds **Job** like Promises, processes.nextTick, etc.

The Event Loop Model prioritizes all the Jobs in JobQueue over anything in TaskQueue
