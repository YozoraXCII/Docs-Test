# Resolution/Edition Overlay

The `resolution` Default Overlay File is used to create an overlay based on the resolutions and editions available on each item within your library.

![](images/resolution.png)

## Requirements & Recommendations

Supported Overlay Level: Movie, Show, Episode

Recommendations: Editions overlay is designed to use the Editions field within Plex [which requires Plex Pass to use] or the [TRaSH Guides](https://trash-guides.info/) filename naming scheme

## Supported Resolutions

| Resolution   | Key          | Weight |
|:-------------|:-------------|:-------|
| 4K HDR10+    | `4k_plus`    | `160`  |
| 4K DV        | `4k_dv`      | `150`  |
| 4K HDR       | `4k_hdr`     | `140`  |
| 4K           | `4k`         | `130`  |
| 1080P HDR10+ | `1080p_plus` | `125`  |
| 1080P DV     | `1080p_dv`   | `120`  |
| 1080P HDR    | `1080p_hdr`  | `110`  |
| 1080P        | `1080p`      | `100`  |
| 720P HDR10+  | `720p_plus`  | `95`   |
| 720P DV      | `720p_dv`    | `90`   |
| 720P HDR     | `720p_hdr`   | `80`   |
| 720P         | `720p`       | `70`   |
| 576P HDR10+  | `576p_plus`  | `65`   |
| 576P DV      | `576p_dv`    | `60`   |
| 576P HDR     | `576p_hdr`   | `50`   |
| 576P         | `576p`       | `40`   |
| 480P HDR10+  | `480p_plus`  | `35`   |
| 480P DV      | `480p_dv`    | `30`   |
| 480P HDR     | `480p_hdr`   | `20`   |
| 480P         | `480p`       | `10`   |
| HDR10+       | `plus`       | `7`    |
| DV           | `dv`         | `5`    |
| HDR          | `hdr`        | `1`    |

## Supported Editions

| Edition             | Key             | Weight |
|:--------------------|:----------------|:-------|
| Extended Edition    | `extended`      | `190`  |
| Uncut Edition       | `uncut`         | `180`  |
| Unrated Edition     | `unrated`       | `170`  |
| Special Edition     | `special`       | `160`  |
| Anniversary Edition | `anniversary`   | `150`  |
| Collector's Edition | `collector`     | `140`  |
| Diamond Edition     | `diamond`       | `130`  |
| Platinum Edition    | `platinum`      | `120`  |
| Director's Cut      | `directors`     | `110`  |
| Final Cut           | `final`         | `100`  |
| International Cut   | `international` | `90`   |
| Theatrical Cut      | `theatrical`    | `80`   |
| Ultimate Cut        | `ultimate`      | `70`   |
| Alternate Cut       | `alternate`     | `60`   |
| Coda Cut            | `coda`          | `50`   |
| IMAX Enhanced       | `enhanced`      | `40`   |
| IMAX                | `imax`          | `30`   |
| Remastered          | `remastered`    | `20`   |
| Criterion           | `criterion`     | `10`   |
| Richard Donner      | `richarddonner` | `9`    |
| Black and Chrome    | `blackchrome`   | `8`    |
| Definitive          | `definitive`    | `7`    |
| Ulysses             | `ulysses`       | `6`    |

## Config

The below YAML in your config.yml will create the overlays:

```yaml
libraries:
  Movies:
    overlay_path:
      - pmm: resolution
  TV Shows:
    overlay_path:
      - pmm: resolution
      - pmm: resolution
        template_variables:
          overlay_level: season
      - pmm: resolution
        template_variables:
          overlay_level: episode
```

## Template Variables

Template Variables can be used to manipulate the file in various ways to slightly change how it works without having to make your own local copy.

Note that the `template_variables:` section only needs to be used if you do want to actually change how the defaults work. Any value not specified is its default value if it has one if not it's just ignored.

All [Shared Overlay Variables](../overlay_variables) are available with the default values below as well as the additional Variables below which can be used to customize the file.

| Variable            | Default     |
|:--------------------|:------------|
| `horizontal_offset` | `15`        |
| `horizontal_align`  | `left`      |
| `vertical_offset`   | `15`        |
| `vertical_align`    | `top`       |
| `back_color`        | `#00000099` |
| `back_radius`       | `30`        |
| `back_width`        | `305`       |
| `back_height`       | `105`/`189` |

| Variable                     | Description & Values                                                                                                                           |
|:-----------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------|
| `use_resolution`             | **Description:** Turns off all Resolution Overlays in the Defaults file.<br>**Values:** `false` to turn off the overlays                       |
| `use_edition`                | **Description:** Turns off all Edition Overlays in the Defaults file.<br>**Values:** `false` to turn off the overlays                          |
| `overlay_level`              | **Description:** Choose the Overlay Level.<br>**Values:** `season` or `episode`                                                                |
| `weight_<<key>>`<sup>1</sup> | **Description:** Controls the weight of the Overlay. Higher numbers have priority. **Only works with Edition keys.**<br>**Values:** Any Number |

1. Each default overlay has a `key` that when calling to effect a specific overlay you must replace `<<key>>` with when calling.

The below is an example config.yml extract with some Template Variables added in to change how the file works.

```yaml
libraries:
  Movies:
    overlay_path:
      - pmm: resolution
        template_variables:
          use_dv: false
          use_hdr: false
          use_1080p: false
          use_720p: false
          use_576p: false
          use_480p: false
          use_1080p_hdr: false
          use_1080p_dv: false
```
