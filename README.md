# Miele Appliance Card for Home Assistant

A washer and tumble dryer card for **Miele** machines that use Home Assistant's built-in
[Miele integration](https://www.home-assistant.io/integrations/miele/).

The machine is drawn on the card with a progress ring round the door, the time left on its display, and the
laundry turning while it runs. You can start, pause, resume and stop a cycle from the card, and switch the machine off.

**📖 [Step-by-step guide and live demo](https://mymediabuild.uk/home-assistant-miele-washer-dryer-card/)** · **☕ [Buy me a coffee](https://buymeacoffee.com/bobgreggr)**

> **Tested on a real Miele washer** (thanks **MrMoep**). I don't own a Miele myself, and the dryer has only been
> tested against simulated states so far. If you have a Miele dryer, please [open an issue](../../issues) with your
> model and what you see.

Sister card of the [hOn washer & dryer card](https://github.com/spikey1965/ha-hon-appliance-card) (Haier, Candy, Hoover)
and the [Candy card](https://github.com/spikey1965/ha-candy-appliance-card) (Candy Simply-Fi).

![Washer running and dryer cooling down](images/running.png)

## What it shows

- Status: Off, On, Ready, Delayed start, Running (with the phase: Washing, Rinse, Spin, Drying, Cooldown ...), Paused, Finished, Error
- Time left on the machine's display, the end time, and a progress ring round the door
- Programme, temperature and spin speed (washer) or dryness (dryer)
- The door: a **Door** line in the info panel (Open, Closed, Locked while it runs) when your machine has a door sensor, and a door icon that turns amber when it's open
- Remote Control
- **English or German**, following Home Assistant's language (programme names use Home Assistant's own translation)
- **Start**, **Pause**, **Resume** and **Stop** (Stop asks first), and **Off** using the machine's power switch

The buttons only show when the machine will take them at that moment. For example, there's no Pause during a delayed start.

![Programme selected, ready to start](images/ready.png)

**Limits that come from the integration and the machine:**
- The buttons only work with **Remote Control** switched on at the machine.
- You can't pick a programme from the card. Miele's integration needs a programme number to start one, and it doesn't
  tell Home Assistant which numbers your machine has. So choose the programme on the machine, then press **Start** on the card.
- No cycle count, because the integration doesn't have one.

## Install

### Marketplace (recommended)

1. Go to **Settings → Marketplace** and click **Add from link**. This asks you to connect GitHub.
2. Paste `https://github.com/spikey1965/ha-miele-appliance-card` and choose the type **Dashboard** if asked.
3. Find **Miele Appliance Card** under **New**, open it and click **Install**. Reload your browser.

The first time you use Marketplace, tick **I understand the risks and agree** and click **Continue**.

**On a version older than 2026.11?** Marketplace is still called HACS there. Use **Download** in place of Install and **⋮ → Custom repositories** in place of Add from link.

**Manual:** copy `miele-appliance-card.js` to `/config/www/`, then add a dashboard resource
(Settings → Dashboards → ⋮ → Resources): `/local/miele-appliance-card.js?v=1.0.0`, type **JavaScript module**.

It can sit alongside the hOn card. They use different card names.

## Use

```yaml
type: custom:miele-appliance-card
appliance: washer
```

```yaml
type: custom:miele-appliance-card
appliance: dryer
```

The card finds your machine by itself: the first Miele washer (or dryer, with `appliance: dryer`). The Miele
integration names its entities in Home Assistant's language (`sensor.waschmaschine_programmphase` in German), so the
card finds them through the integration instead of by name, and it works in any language.

If you have more than one Miele washer or dryer, set `entity` to the machine's status sensor, the one with no ending,
such as `sensor.washing_machine` or `sensor.waschmaschine`.

| Option | Default | What it does |
|---|---|---|
| `appliance` | `washer` | `washer` or `dryer` |
| `entity` | first Miele machine | the machine's status sensor, e.g. `sensor.waschmaschine` |
| `name` | Washer / Dryer (Waschmaschine / Trockner in German) | card title |
| `colour` | blue / orange | accent colour, e.g. `"#4fb3ff"` |
| `style` | `drawn` | `photo` = a more detailed illustration |
| `finish` | `white` | machine colour: `white`, `graphite` or `black` |
| `max_width` | `440px` | |
| `images` | built in | a folder with your own `washer.svg`, `dryer.svg` and `laundry-drum.webp` |
| `language` | `auto` | `auto` follows Home Assistant's language (German or English); `en` or `de` to choose |

![Photo style in black](images/black.png)

## Troubleshooting

- **No buttons:** switch Remote Control on at the machine. Pause, Resume and Stop also hide when the machine says it
  won't take them right now.
- **Card shows Off and "—" everywhere:** the card didn't find a Miele washer (or dryer). Set `entity` to the machine's
  status sensor (Developer Tools → States, search for your machine's name).
- **Something else looks wrong:** please open an issue with your model and a screenshot of Developer Tools → States
  filtered for your machine.

## Support and requests

I build and look after this card in my spare time.

- **Found a bug?** [Open an issue](../../issues/new/choose) and fill in the form. A screenshot and the entity list help a lot.
- **Want another brand or integration?** Pull requests are very welcome. I can only test machines I own, so I can't promise to add new ones myself. Use the "Support for another machine" form so all the details are in one place.
- **Like the card?** A ⭐ on GitHub helps other people find it, and you can [buy me a coffee](https://buymeacoffee.com/bobgreggr) ☕. More free Home Assistant cards and guides at [mymediabuild.uk](https://mymediabuild.uk).

## Thanks

Built from **MrMoep**'s detailed write-up of the Miele entities on the hOn card's issue tracker, and tested by him
on his own Miele washer (the Door line was his idea).
Card by [My Media Build](https://mymediabuild.uk), with a [step-by-step guide](https://mymediabuild.uk/home-assistant-miele-washer-dryer-card/).
If you find it useful, you can [buy me a coffee](https://buymeacoffee.com/bobgreggr) ☕ (no pressure).

## Licence

MIT. Not affiliated with or endorsed by Miele.
