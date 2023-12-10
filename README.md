# SSBU Modding with Smashline

## Purpose

To create a workspace that will facilitate developing mods for Super Smash Bros Ultimate.
Currently geared towards Smashline 2.

## Assumptions

1. A Unix-based OS. I use Windows Subsystem Linux with Ubuntu exclusively for programming, and if you wish to pursue programming as a job, you'll need to learn Linux eventually.
2. You have [Rust](https://www.rust-lang.org/tools/install) installed, as that's our language of choice for developing mods.
3. You have [Task](https://taskfile.dev/installation/) installed, so you can interact with the `Taskfile`.
4. You have `git`, for reasons that should be known.
5. You have `curl` (should come with Unix and Windows).

## How to install

It's as simple as running

```bash
task
```
No extra arguments needed. That will run the `default` task dedicated to installing everything for you.

If you encounter a failure anywhere in the installation process and want to redo the
installation in it's entirely, simply run:

```bash
task default --force
```

If you want to perform each step one at a time, all available tasks are available with:

```bash
task --list
```

## So how do I use this repo?

The `dev/` folder contains most of the items you need to begin work on your mod, but
you will need to do the following:

1. Copy `Cargo.toml`, `Cargo.lock` and `rust-toolchain` from `skyline-rs-template` to `dev/`.
2. Give your project a unique name in the `Cargo.toml` file.
3. Make the directory `dev/src`
4. Copy `skyline-rs-template/src/lib.rs` into `dev/src/`.
5. Modify `dev/src/lib.rs` to the following skeleton:

```rust
#![feature(concat_idents, proc_macro_hygiene)]
#![allow(unused_macros)]


#[skyline::main(name = "my_new_project")]  // Change `my_new_project` to whatever you want.
pub fn main() {}
```

Now, you have your environment set up to start your modding! If you're having trouble
writing a mod, be sure to peek at `skyline-rs-template/` for help on how the "final"
structure should look like.

I also included a separate `Taskfile` with it's own suite of uses. In order to use it,
you will have to:

1. Make a copy of `env.yml.template` and name it `env.yml`.
2. Populate all keys under the `vars` key in `env.yml`.

This will enable you to use commands such as `task dev:deploy` so you don't have to
look for your `.nro` file to deploy to your skyline plugins, it will do it for you!

## Post install file breakdown

### Dumps

#### SSBU-Dumped-Scripts

Contains all matters of attributes that make up a fighter's actions. Effects, expressions,
sounds, active hitbox data, etc. These are the files you'd go to if you're looking to
change things such as how a fighter's move works or setting global rules all fighters
abide by (i.e. turbo mode.)

[Click here for a video tutorial](https://youtu.be/iypFEqluC68?si=rXGyaoDM3-F6oWnD&t=14)

#### SSBU-Dumped-Motion-Lists

View the decompiled `motion_list.bin` files for every character as `motion_list.yml`
files. Especially useful when you want to do things like port moves from different
characters, or add moves into a character's repetoire.

[Click here for a video tutorial on porting moves.](https://www.youtube.com/watch?v=X1Gz-Lrt1H8)
Just keep in mind that you already contain the decompiled `motion_list.bin` file thanks
to this dump.

### Rust files

#### `cpp.rs` source file

Think of it like a header file in C++, containing all function definitions available to
you.

#### `lua_const.rs` source file

A hashmap / dictionary of every constant value in SSBU.

#### `tale_const.rs` source file

A global table for various attributes regarding a fighter's current / past status.

[Click here for a video tutorial](https://youtu.be/cle-8CWnnls?si=i9ceVhkyqag-LHBh&t=41)


### `CSV` files

#### `animation_animcmd*.csv`

Contains a list of all animation names, as well as their in-game animcd equivalents.

#### `ParamLabels.csv` hash list

Contains almost every single hash value in SSBU. Special moves, camera effects, backgrounds,
etc.


## Non-repo resources

For developing smashline plugins, [this documentation page is the single most useful thing](https://ultimate-research.github.io/skyline-rs-template/doc/smash/index.html). It contains useful pieces of information such as every function definition available to smashline and hashes for almost every value used in SSBU.


## Commendations Page

Thank you to [`Lily Lambda λ`](https://github.com/LilyLavender) for her [Ultimate Modding Workshop](https://www.youtube.com/watch?v=02NaFwNcC3M&list=PLJ8C0Hk2ZKHvxjfFylRUIbVnDUvxLdejh&pp=iAQB) video series.

Thank you to [`WuBoytH`](https://github.com/WuBoytH) for providing the Smashline templates.

Thank you to [`The Smash Ultimate Research Group`](https://github.com/ultimate-research) for providing the ability to mod with Skyline in the first place,
and for providing all of the hashes SSBU uses.

Thank you to the user who [created this Google Spreadsheet](https://docs.google.com/spreadsheets/d/1q_TpWoQkr9YWgQ7fc3JpHuU9zKfCLtl80Uodcyc0NPY/edit#gid=0) including all animations, which I transformed into two csv files checked in this repo.

Thank you to the [SSBU Modding Discord server](https://discord.com/invite/ASJyTrZ) for their (continued) assistance in creating mods.


And finally, thank you to all of the modders out there, whose creations led me to start
modding in the first place.
