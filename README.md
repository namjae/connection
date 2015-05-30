Connection
==========

Prototype of `Connection` behaviour. The API is similar to the GenServer
API. There are 2 additional callbacks `connect/2` and `disconnect/2`:

```elixir
  defcallback init(any) ::
    {:connect, any, any} |
    {:noconnect, any} | {:noconnect, any, timeout | :hibernate} |
    {:backoff, timeout, any} | {:backoff, timeout, any, timeout | :hibernate} |
    :ignore | {:stop, any}

  defcallback connect(any, any) ::
    {:ok, any} | {:ok, any, timeout | :hibernate} |
    {:backoff, timeout, any} | {:backoff, timeout, any, timeout | :hibernate} |
    {:stop, any, any}

  defcallback disconnect(any, any) ::
    {:connect, any, any} |
    {:noconnect, any} | {:noconnect, any, timeout | :hibernate} |
    {:backoff, timeout, any} | {:backoff, timeout, any, timeout | :hibernate} |
    {:stop, any, any}

  defcallback handle_call(any, {pid, any}, any) ::
    {:reply, any, any} | {:reply, any, any, timeout | :hibernate} |
    {:noreply, any} | {:noreply, any, timeout | :hibernate} |
    {:disconnect | :connect, any, any} |
    {:disconnect | :connect, any, any, any} |
    {:stop, any, any} | {:stop, any, any, any}

  defcallback handle_info(any, any) ::
    {:noreply, any} | {:noreply, any, timeout | :hibernate} |
    {:disconnect | :connect, any, any} |
    {:stop, any, any}

  defcallback code_change(any, any, any) :: {:ok, any}

  defcallback terminate(any, any) :: any
```
There is an example of a simple TCP connection process in
`examples/tcp_connection/`.
