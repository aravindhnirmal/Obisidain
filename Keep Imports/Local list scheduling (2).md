[[Keep/Colour/DEFAULT]] [[Keep/Attachments]] [[Keep/Archived]] 

instructions = [    "Load r1,@a",    "add r2,r1,r1",    "load r3,@b",    "mult r4,r3,r2"]

deps = {
    0: set(),
    1: {0},
    2: set(),
    3: {1, 2}
}

latencies = {
    "Load": 3,
    "add": 1,
    "mult": 2
}

schedule = {}
cycle = 0

while len(schedule) < len(instructions):
    for i in range(len(instructions)):
        if i in schedule:
            continue
        if deps[i].issubset(schedule.keys()):
            schedule[i] = cycle
            cycle += latencies[instructions[i].split()[0]]

for i in range(len(instructions)):
    print(f"Cycle {schedule[i]}: {instructions[i]}")



![[187d7653634.a9b23b5417379f5b.jpg]]