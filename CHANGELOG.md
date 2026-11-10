# CHANGELOG

## 0.1.49

- `brizz.decision_call()`, `brizz.adecision_call()` and `brizz.record_decision_call()` trace calls to classification models that your own code makes. Requires a Brizz backend that reads decision calls; calls sent to an older one are not shown with their answers, and are priced only when you set their cost.

## 0.1.48

- More precise PII masking: long numbers that aren't card numbers are left intact.
- Quieter startup and shutdown logs: libraries your app doesn't use are skipped silently.

## 0.1.47

- `set_global_tracer_provider=False` keeps Brizz spans on their own provider, alongside your own OpenTelemetry setup.
- `Brizz.flush()` and `Brizz.aflush()` send queued telemetry without shutting down.
- `brizz.get_tracer_provider()` for instrumentations you construct yourself.

## 0.1.46

- LangChain chains and LangGraph agents on the OpenAI SDK record each model call once instead of twice.

## 0.1.45

- Calls to TypeSafe models such as Jev are traced: each call records the state, the questions and the answers.
- Masking leaves numbers and booleans unchanged unless a rule actually masks part of them.
- A library that fails to load no longer stops the libraries after it from being instrumented.
- LangChain spans record reasoning tokens (Gemini thinking, OpenAI reasoning).

## 0.1.44

- Default masking leaves identifiers, custom properties and numeric values unchanged.

## 0.1.43

- MCP servers on FastMCP 4 (`mcp` 2.x) keep their sessions and user identity.

## 0.1.42

- `record_metric` accepts `scope="trace"`, so a metric reported once per turn keeps one value per turn; the session reads as the average of its turns.

## 0.1.41

- `record_metric` accepts `service_name` and `trace_id`, so one process can score conversations from many services, and attach a score by trace when the session id isn't at hand.

## 0.1.40

- Improve LangGraph tracing for conversations that resume from an earlier point.

## 0.1.39

- Bound the final telemetry flush at shutdown and at process exit, so a slow or unreachable endpoint no longer holds up the process. Tune with `shutdown_timeout`.
- Add `Brizz.ashutdown()` for async applications.

## 0.1.38

- Fix session, user and organization context being dropped when a scoped helper is handed an async function.

## 0.1.37

- Support OpenTelemetry 1.40 through 1.44.

## 0.1.36

- Add `brizz.agent()`, `@brizz.agent_context()` and `brizz.set_agent()` to mark work that runs as a subagent, so its conversation shows as its own lane instead of mixing into the main transcript. Works when the subagent runs in a background job too.

## 0.1.35

- Add session tracking for stateless MCP servers. Tool calls from one client now group into a single session, with an optional note of what the caller was trying to do. Off by default; enable with `mcp_session_tracking`.

## 0.1.34

- Add LiveKit Agents support. Voice sessions are traced automatically once the SDK is initialized.

## 0.1.33

- Remove `lancedb` as a required dependency to reduce install size.

## 0.1.32

- Add a `tools` option to `mute()` / `amute()` to hide or keep tool calls independently of the assistant reply. Requires a Brizz backend that understands `brizz.mute.tools`; against an older one, the tools-only form (`mute(input=False, output=False, tools=True)`) mutes nothing.

## 0.1.31

- Add `before_send_span` to drop spans before they are sent.

## 0.1.30

- Add `record_metric` to report your own scores and measurements on a conversation.

## 0.1.29

- Add typed setters to identify users, organizations, and messages.
- Add `record_feedback` to capture end-user reactions on a message or conversation.

## 0.1.28

- Attach external links to a session.

## 0.1.27

- Add `mute()` / `amute()` to omit user and/or assistant content for calls made within a block.

## 0.1.26

- Lighter requirements.

## 0.1.25

- Improved SDK robustness when used before initialization.

## 0.1.24

- Internal refinement to MCP tool-registration instrumentation.

## 0.1.23

- PII masking improvements.

## 0.1.22

- `Session.set_input` / `Session.set_output` now also set the Langfuse input/output span attributes (`langfuse.observation.input/output`, `langfuse.trace.input/output`) so the `brizz.start_session` trace renders Input/Output in Langfuse.

## 0.1.21

- Add `dsn` / `BRIZZ_DSN` support for Brizz Server DSN configuration

## 0.1.20

- Add Claude Agent SDK instrumentation

## 0.1.19

- Add MCP schema instrumentation support

## 0.1.18

- Extend `Session.set_input` / `Session.set_output` to accept per-turn context via `**kwargs` (or an optional `context` dict). Each call now appends both the text and a context bag to parallel index-aligned span attributes `brizz.session.input.context` / `brizz.session.output.context`; the dashboard renders the bag under a collapsible Context panel on that turn's message.

## 0.1.17

- Add fastmcp instrumentation

## 0.1.16

- Add `disable_span_exporter` option (also via `BRIZZ_DISABLE_SPAN_EXPORTER=true` env var) to skip span exporter/processor/`TracerProvider` setup entirely. Useful for dev/test environments where you want to keep `Brizz.initialize()` in code without sending telemetry.

## 0.1.15

- Add `start_session_title()` / `astart_session_title()` to exclude title generation LLM calls from conversation view
- Add `mode='title'` parameter to `start_session()` / `astart_session()`
- Add `Session.set_title()`

## 0.1.14
- Support Python 3.14

## 0.1.12

- Add `get_active_session()` to retrieve the current session without passing it explicitly

## 0.1.11

- Add support for Agno SDK

## 0.1.10

- Upgraded to opentelemetry-python 1.39.1

## 0.1.9

- Fix Langfuse and Brizz SDK co-existing

## 0.1.8.post1

- Removed MCP instrumentation (`opentelemetry-instrumentation-mcp` dependency)

## 0.1.8

- Remove `mcp` from default instrumentation

## 0.1.7

- Add `set_input`, `set_output` and `update_properties` to session.

## 0.1.6

- Add `blocked_instrumentations` configuration to selectively disable instrumentations

## 0.1.5

- Add support for custom properties

## 0.1.4

- Support OpenAI v1

## 0.1.3

- Add SDK version tags to ResourceAttributes

## v0.1.2 (2025-09-04)

- Added optional `environment` parameter to SDK initialization for deployment environment tagging

## v0.1.1 (2025-08-25)

- Fixed DependencyConflict with non-instrumented installed packages
- Disabled CrewAI auto instrumentation for Python SDK

## v0.1.0 (2025-08-01)

- Initial Release
