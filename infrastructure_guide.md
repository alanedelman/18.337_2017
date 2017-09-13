# Infrastructure Guide for 18.337/6.338

During the course we will be using AWS for a preconfigured environment that
provides a GPU for all students. Secondly you will get access to Anubis a
shared memory node. Please follow the instructions below to get access
to both systems.

## Anubis

Anubis is a shared memory node hosted and maintained by the Julia community
(see https://github.com/Keno/anubis.juliacomputing.io). In order to get access
you need to do the following steps.

1. Create an account on Github.
2. Add your SSH key to that acount. Without this step we won't be able to give
    you access to Anubis. See https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/
3. Fillup the signup form: https://goo.gl/LYfZSt
4. Read https://github.com/Keno/anubis.juliacomputing.io/blob/master/README
   for information about the machine.

Once you have done this you will be able to access Anubis (this make take a day or two to process for us)
at `anubis.juliacomputing.io` via `ssh`. Do note that your username is your Github
account name.

## AWS

For students who don't have a GPU available in their computer we recommend using
AWS to get access to a GPU instance. AWS provides students with a $100 credit
through awseducate.com. This should be enough to get you started.

AWS is Amazons public cloud, be aware that resources you are using will be billed
and you should stop your instances if you are not using them.

1. Signup to AWS on https://aws.amazon.com/
2. Use https://awseducate.com with your mit.edu email to get a $100 credit and apply that credit to your account.
3. Use the region `us-east-1` for everything! https://console.aws.amazon.com/console/home?region=us-east-1
4. Check that your credit has been applied under https://console.aws.amazon.com/billing/home?region=us-east-1#/credits
5. Launch an EC2 instance with the AMI *MIT-JuliaGPU* (under community) on an `p2.xlarge` instance (GPU compute)
6. Check that you have:
    1. a public DNS address
    2. downloaded the private key associated to that instance
    3. move that private key to `~.ssh/`
    4. and do `chmod 400 .ssh/$AWSKEY.pem`
7. You should now be able to access your personal instance via
   `ssh -i .ssh/$AWSKEY.pem ubuntu@$PUBLIC_DNS`
8. Don't delete the directory `$HOME/julia`
9. Enter `julia` to start a julia process

To launch a Jupyter notebook your currently have to do the following:

```
ssh -i .ssh/$AWSKEY.pem -L 8080:localhost:8080 ubuntu@$PUBLIC_DNS
> julia
julia> using IJulia
julia> notebook(detached=true)
julia> run(`$(IJulia.notebook_cmd[1]) notebook list`)
# Get the token used by the instance bound to localhost:8888
# and visit localhost:8888 in your browser and past the token their
```

### Note:
You can switch to a shell mode in the Julia REPL by pressing `;` or execute programs with `run(\`echo "Hello World!"\`)`

to terminate all Jupyter instances running use `killall jupyter-notebook`

### Notes on the AMI

The AMI currently comes installed with:
- Julia 0.6 with GPU support
- CUDA 8.0 and CUDNN 7.0
- The Julia packages
  - CUDAnative.jl
  - GPUArrays.jl
  - IJulia.jl/Jupyter
  - Plots.jl/PlotlyJS.jl
  - CXX.jl
- tmux/htop

Also note that `SpecialFunctions.jl` is currently pinned due to https://github.com/JuliaMath/SpecialFunctions.jl/issues/50
and that the AMI will be updated regularly during the course.
