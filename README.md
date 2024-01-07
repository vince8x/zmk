# ZMK Firmware: Personal fork

This is my personal ZMK fork containing various experimental features used in
my [zmk-config](https://github.com/urob/zmk-config/). This particular branch
contains a backport by Cem Aksoylar that ports the new pointer API in
[#2027](https://github.com/zmkfirmware/zmk/pull/2027) to Zephyr 3.2. The branch
is transitional and will be retired once the new API is merged into upstream.

Note that if you are switching to the new pointer API from the [original mouse
PR](https://github.com/zmkfirmware/zmk/pull/778), then the following
adjustments are necessary in your `zmk-config`:

- `&mwh` --> `&msc`
- `MOVE_VERT` --> `MOVE_Y`
- `MOVE_HOR` --> `MOVE_X`
- `SCROLL_VERT` --> `SCRL_Y`
- `SCROLL_HOR` --> `SCRL_X`

E.g., this is my current [mouse
configuration](https://github.com/urob/zmk-config/blob/upstream-mouse/config/mouse.dtsi)
using the new api.

---

Below is a list of features currently included in this branch _on top of_
the official ZMK master branch.

- **pointer movement/scrolling** - [backport](https://github.com/caksoylar/zmk/tree/feat/mouse-keys-3.2) of #2027 by Cem Aksoylar
- **swapper** (PR [#1366](https://github.com/zmkfirmware/zmk/pull/1366)) - official PR + fixes needed for Zephyr 3.2
- **smart-word** (PR [#1451](https://github.com/zmkfirmware/zmk/pull/1451)) - official PR, updated to Zephyr-3.2
- **fix-key-repeat** - fix [key-repeat rolling issue](https://github.com/zmkfirmware/zmk/issues/1207)
- **on-release-for-tap-preferred** - [on-release option for tap-preferred](https://github.com/celejewski/zmk/commit/d7a8482712d87963e59b74238667346221199293) by Andrzej
- **zen-tweaks** - [display & battery improvements](https://github.com/caksoylar/zmk/tree/caksoylar/zen-v1%2Bv2) by Cem Aksoylar

In order to use this branch with Github Actions, replace the contents of `west.yml` in
your `zmk-config/config` directory with the following contents:

```
manifest:
  remotes:
    - name: urob
      url-base: https://github.com/urob
  projects:
    - name: zmk
      remote: urob
      revision: main
      import: app/west.yml
  self:
    path: config
```
