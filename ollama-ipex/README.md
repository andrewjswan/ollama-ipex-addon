<div align="center">
<h1>Ollama IPEX Add-on for Home Assistant</h1>
</div>

## General

[![ha addon_badge](https://img.shields.io/badge/HA-Addon-blue.svg)](https://developers.home-assistant.io/docs/add-ons)
[![Ollama IPEX](https://img.shields.io/static/v1?label=Ollama&message=IPEX&color=blue&logo=ollama)](https://github.com/andrewjswan/ollama-ipex-addon/)
[![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/andrewjswan/ollama-ipex-addon/build.yml?logo=github)](https://github.com/andrewjswan/ollama-ipex-addon/actions)
[![GitHub release (latest SemVer including pre-releases)](https://img.shields.io/github/v/release/andrewjswan/ollama-ipex-addon?include_prereleases)](https://github.com/andrewjswan/ollama-ipex-addon/blob/master/esphome-update/CHANGELOG.md)
[![GitHub License](https://img.shields.io/github/license/andrewjswan/ollama-ipex-addon?color=blue)](https://github.com/andrewjswan/ollama-ipex-addon/blob/master/LICENSE)
[![StandWithUkraine](https://raw.githubusercontent.com/vshymanskyy/StandWithUkraine/main/badges/StandWithUkraine.svg)](https://github.com/vshymanskyy/StandWithUkraine/blob/main/docs/README.md)

Ollama Portable on Intel GPU with IPEX-LLM.

## Model Directory

All downloaded models are stored `/share/ollama` by default. For historic reasons you can also configure it for `/config/ollama`. Please make sure that you have sufficient space available.

## Ollama Integration

To download any models either use the API of Ollama or integrate with the Home Assistant Integration [Ollama](https://www.home-assistant.io/integrations/ollama/):

[![Add Ollama Integration](https://my.home-assistant.io/badges/brand.svg)](https://my.home-assistant.io/redirect/config_flow_start/?domain=ollama)

Use the following data:

- URL: `http://addon-slug:11434`

If you want to change the model, delete the integration (not the addon!) and restart the process for the configuration of the integration.

## Note on the UI Link

The UI Link is only there to check if the API of ollama is available. There is no chat functionality included in the official image of ollama.
