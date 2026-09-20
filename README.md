# Maxey0 Observability Boundary Lab

A runnable research harness for testing whether a multi-agent execution plane is bounded by an observable, assignable, controllable and enforceable SCW0 address space.

## Architecture

- **SCW0**: supervisory/control plane. Creates SCWs, assigns agents, mediates synthetic state-changing capabilities, and records a hash-linked event chain.
- **Execution plane**: Maxey1, Maxey2, and a red-team boundary breaker. Dependent, independent and interdependent loop edges are represented in the event stream.
- **Adversarial test**: the breaker discovers an intentionally unregistered `ambient-temp-host` capability. With SCW0 enabled, the capability is converted to a denial at the enforcement boundary. In counterfactual mode, the same capability becomes an actual `BYPASS` event, demonstrating the observability gap.
- **OpenAI Agents SDK**: when `OPENAI_API_KEY` is present, the server additionally runs a live Agents SDK smoke test using function tools, handoffs, and hosted web search. All local state-changing tools are synthetic.

## Run

```bash
npm install
npm run dev
```

Open `http://localhost:5173`.

For a live Agents SDK run, configure `OPENAI_API_KEY` in the server environment. Without it, the deterministic execution-plane test still runs and the dashboard remains fully usable.

## Tests

The dashboard tests:

1. bounded address space: agent → SCW → authorization → capability → state transition → authoritative event;
2. handoff/message/resource edges;
3. dependent, independent and interdependent loop relationships;
4. adversarial discovery of a capability below/beside/outside SCW0;
5. hash-chain replay integrity;
6. counterfactual same-level orchestration without SCW0.

The harness intentionally uses synthetic resources and channels. It does not expose real credentials, shells, filesystem writes, arbitrary network sockets, or destructive external actions to the agents.
