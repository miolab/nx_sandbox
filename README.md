# Nx Sandbox

Code sandbox for **Nx**

> Nx is a multi-dimensional tensors library for Elixir with multi-staged compilation to the CPU/GPU.  
> (https://github.com/elixir-nx/nx)

## Usage

### Set up (Elixir / Erlang OTP)

```sh
$ docker-compose build
```

#### **Usage** IEx

```sh
$ docker-compose up -d
```

```sh
$ docker-compose exec app iex

Erlang/OTP 24 [erts-12.0.2] [source] [64-bit] [smp:4:4] [ds:4:4:10] [async-threads:1] [jit]
Interactive Elixir (1.12.1) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)>
```

### Set up (Nx)

- execute `mix new app_name`

  ```sh
  $ docker-compose run --rm app mix new . --app my_app

  Creating nx_sandbox_app_run ... done
  * creating README.md
  * creating .formatter.exs
  * creating .gitignore
  * creating mix.exs
  * creating lib
  * creating lib/my_app.ex
  * creating test
  * creating test/test_helper.exs
  * creating test/my_app_test.exs

  Your Mix project was created successfully.
  You can use "mix" to compile it, test it, and more:

      mix test

  Run "mix help" for more commands.
  ```

- update file `mix.exs`

  ```elixir
  defp deps do
    [
      {:nx, "~> 0.1.0-dev", github: "elixir-nx/nx", branch: "main", sparse: "nx"}  # --> add
      ...
  ```

- execute `mix deps.get`

  ```sh
  $ docker-compose run --rm app mix deps.get

  Creating nx_sandbox_app_run ... done
  * Getting nx (https://github.com/elixir-nx/nx.git - origin/ main)
  remote: Enumerating objects: 9111, done.
  remote: Counting objects: 100% (1317/1317), done.
  remote: Compressing objects: 100% (668/668), done.
  remote: Total 9111 (delta 770), reused 1103 (delta 621),  pack-reused 7794
  Receiving objects: 100% (9111/9111), 40.19 MiB | 1.97 MiB/  s, done.
  Resolving deltas: 100% (5937/5937), done.
  ```

- execute `mix test`

  ```sh
  $ docker-compose run --rm app mix test

  Creating nx_sandbox_app_run ... done
  ==> nx
  Compiling 20 files (.ex)
  Generated nx app
  ==> my_app
  Compiling 1 file (.ex)
  Generated my_app app
  ..

  Finished in 0.06 seconds (0.00s async, 0.06s sync)
  1 doctest, 1 test, 0 failures

  Randomized with seed 559301
  ```

### **Usage** Nx with IEx

```sh
$ docker-compose up -d

$ docker-compose exec app iex -S mix

Erlang/OTP 24 [erts-12.0.2] [source] [64-bit] [smp:4:4] [ds:4:4:10]   [async-threads:1] [jit]

==> nx
Compiling 20 files (.ex)
Generated nx app
==> my_app
Compiling 1 file (.ex)
Generated my_app app
Interactive Elixir (1.12.1) - press Ctrl+C to exit (type h() ENTER for help)

iex(1)>t = Nx.tensor([[1, 2], [3, 4]])
#Nx.Tensor<
  s64[2][2]
  [
    [1, 2],
    [3, 4]
  ]
>
iex(2)> Nx.shape(t)
{2, 2}
>
iex(3)> Nx.divide(Nx.exp(t), Nx.sum(Nx.exp(t)))
#Nx.Tensor<
  f32[2][2]
  [
    [0.032058604061603546, 0.08714432269334793],
    [0.23688282072544098, 0.6439142227172852]
  ]
>
```

---

## Ref

https://hub.docker.com/_/elixir

https://github.com/elixir-nx/livebook
