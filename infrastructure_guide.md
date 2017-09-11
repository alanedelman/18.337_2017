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
at `anubis.juliacomuting.io` via `ssh`. Do note that your username is your Github
account name.
