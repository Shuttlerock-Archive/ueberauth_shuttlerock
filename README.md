# Überauth Shuttlerock
[![License][license-img]][license]

[license-img]: http://img.shields.io/badge/license-apache-brightgreen.svg
[license]: https://opensource.org/licenses/Apache-2.0

> Shuttlerock OAuth2 strategy for Überauth.

## Installation

1. Setup your application at [Shuttlerock Developers](https://login.shuttlerock.com/).

1. Add `:ueberauth_shuttlerock` to your list of dependencies in `mix.exs`:

    ```elixir
    def deps do
      [{:ueberauth_shuttlerock, "~> 0.1"}]
    end
    ```

1. Add the strategy to your applications:

    ```elixir
    def application do
      [applications: [:ueberauth_shuttlerock]]
    end
    ```

1. Add Shuttlerock to your Überauth configuration:

    ```elixir
    config :ueberauth, Ueberauth,
      providers: [
        shuttlerock: {Ueberauth.Strategy.shuttlerock, []}
      ]
    ```

1.  Update your provider configuration:

    ```elixir
    config :ueberauth, Ueberauth.Strategy.Shuttlerock.OAuth,
      client_id: System.get_env("SHUTTLEROCK_CLIENT_ID"),
      client_secret: System.get_env("SHUTTLEROCK_CLIENT_SECRET")
    ```

1.  Include the Überauth plug in your controller:

    ```elixir
    defmodule MyApp.AuthController do
      use MyApp.Web, :controller
      plug Ueberauth
      ...
    end
    ```

1.  Create the request and callback routes if you haven't already:

    ```elixir
    scope "/auth", MyApp do
      pipe_through :browser

      get "/:provider", AuthController, :request
      get "/:provider/callback", AuthController, :callback
    end
    ```

1. Your controller needs to implement callbacks to deal with `Ueberauth.Auth` and `Ueberauth.Failure` responses.

For an example implementation see the [Überauth Example](https://github.com/ueberauth/ueberauth_example) application.


## License

Please see [LICENSE](https://github.com/Shuttlerock/ueberauth_shuttlerock/blob/master/LICENSE) for licensing details.
