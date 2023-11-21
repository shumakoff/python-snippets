## How to merge list of dictionaries into a single dictionary, putting values of keys into a list, i.e. turn
```
foo = [
    {'a': 'x', 'b': 'y', 'c': 'z'},
    {'a': 'j', 'c': 'z'}
]
```
into 
```
bar = {
    'a': ['x', 'j'],
    'b': ['y', None],
    'c': ['z', 'z']
}
```

```
bar = {
    k: [d.get(k) for d in foo]
    for k in set().union(*foo)
}
```

## Simple python to script that executes <command with args> N times and gives overall average runtime, with runtime for each step
```
import subprocess
import time
import sys

def measure_time(command, num_runs):
    total_time = 0

    for i in range(1, num_runs + 1):
        print(f"Running iteration {i}...")
        start_time = time.time()
        subprocess.run(command, shell=True, stdout=subprocess.DEVNULL, stderr=subprocess.DEVNULL)
        end_time = time.time()
        elapsed_time = end_time - start_time
        print(f"Iteration {i} took {elapsed_time:.6f} seconds")
        total_time += elapsed_time

    average_time = total_time / num_runs

    minutes = int(average_time // 60)
    seconds = int(average_time % 60)
    milliseconds = int((average_time % 1) * 1000)

    print(f"Average time for {num_runs} runs: {minutes} minutes, {seconds} seconds, {milliseconds} milliseconds")

if __name__ == "__main__":
    if len(sys.argv) < 3:
        print("Usage: python script.py '<command>' <num_runs>")
        sys.exit(1)

    command = sys.argv[1]
    num_runs = int(sys.argv[2])

    measure_time(command, num_runs)
```
