# new lab sealed secrets / alternatives to secrets

# new lab PSP alternatives -> kyverno, opa

# new lab specific debug container lab => new feature in K8s debug containers

# new lab (copy the one from 7sins talk) for schedulung - resource requests and limits

# simple authorization lab in here

# make use of training application instead of nginx all the time

# secrets&CM

- multiple env vars without lots env vars
- stringdata versus data
- config file with defined name and more than one config

# port forward on port 80 does not work in codespaces

port 80 is taken by codespaces itself
do this on all trainings

# Terminal linebreak issue

hint in all trainings...
> Note if the terminal is starting to behave strangely you can enter `reset`.

# jobs, was wenn der job nicht terminiert

maxexecutiontime -> activeDeadlineSeconds

# affinities

topologykey -> explain

# another way of influencing scheduling

check https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/
