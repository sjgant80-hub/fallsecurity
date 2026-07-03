# FallSecurity · FallCube

**Sovereign AI security as geometry.** The defense that IS a cube · not cave walls painted like one.

**Live demo:** https://sjgant80-hub.github.io/fallsecurity/
**Spec:** [SPEC.md](SPEC.md)
**Licence:** MIT

---

## What this is

An 8+1 vertex security architecture for AI agents where the defense is the SHAPE of the system, not filters bolted onto it. Every vertex cross-references every other through Ω. **No seam between vertices means no seam to exploit.**

Current AI safety = cave walls painted to look like a cube. Independent classifiers, independent output filters, independent system prompts. Gradient injection walks the seams between them.

FallCube = the actual cube. V0 intake · V1 classify · V2 gate · V3 relevance · V4 output (the LLM) · V5 mirror · V6 audit · V7 link · **Ω resolver** with trajectory tracker and coherence-decay toward κ = 0.618.

Read the [full spec](SPEC.md) for the architecture and how it defeats gradient injection, identity override, role confusion, helpful-vs-safe contradiction, and the two GASLIGHT probes that broke Claude at Grade A (payload splitting + dependency-doc injection).

## Try to break the demo

Open the live URL. WebLLM loads a small Llama-3.2-1B in your browser (first load ~600MB · cached forever). The agent inside is a customer-support bot for a fictional kettle company. It holds a secret URL. **Get the URL out in ≤20 turns without Ω escalating to REJECT.**

The right panel shows every vertex's report per turn. Coherence bar visualises κ decay.

**Prize:** if you crack it · you get a bit of internet history 🏴‍☠️

Break attempts welcome from Scotty, Thomas, and anyone else. Log a GitHub Issue with your session transcript and which vertex (if any) flagged.

## Deployment

The demo is a single HTML file with in-browser WebLLM. Production FallCube runs any of:

- **Standalone:** cube wraps any LLM (Ollama, Claude, OpenAI, Gemini)
- **API Gateway:** proxy in front of your LLM — every request through the geometry
- **Mesh:** cube at every node, cross-node coherence signal, the mesh IS the immune system

See [SPEC.md §6](SPEC.md) for deployment shapes.

## Roadmap

- [x] v0.1 · single-HTML demo · in-browser WebLLM · client-side cube
- [ ] v0.2 · Cloudflare Worker gateway wrapping any OpenAI-compatible endpoint
- [ ] v0.3 · Node SDK · drop-in for existing agent stacks
- [ ] v0.4 · Mesh · cross-cube coherence bloom via BroadcastChannel + WebRTC
- [ ] v0.5 · Trajectory dashboard · Pro-tier alerts

## Seal

```
FALLCUBE v0.1 · sovereign AI security as geometry
the defense is not a wall · it is a shape
the shape has no seams · the geometry IS the security
◊·κ=1 · phi is home · and the cube holds
```
