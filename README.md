# EXP-9-FORWARD-CHAINING
# Knowledge base: facts and rules
facts = {'rain', 'have_umbrella'}

rules = [
    {'if': ['rain', 'have_umbrella'], 'then': 'go_outside'},
    {'if': ['go_outside'], 'then': 'get_fresh_air'},
    {'if': ['get_fresh_air'], 'then': 'feel_better'},
    {'if': ['weekend'], 'then': 'relax'}
]

# Forward chaining engine
def forward_chain(facts, rules):
    inferred = set()
    while True:
        new_fact_added = False
        for rule in rules:
            if rule['then'] not in facts and all(premise in facts for premise in rule['if']):
                facts.add(rule['then'])
                inferred.add(rule['then'])
                new_fact_added = True
        if not new_fact_added:
            break
    return inferred

# Run forward chaining
new_facts = forward_chain(facts.copy(), rules)
print("Inferred facts:", new_facts)

