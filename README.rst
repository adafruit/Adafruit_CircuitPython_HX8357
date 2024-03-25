Introduction
============

.. image:: https://readthedocs.org/projects/adafruit-circuitpython-hx8357/badge/?version=latest
    :target: https://docs.circuitpython.org/projects/hx8357/en/latest/
    :alt: Documentation Status

.. image:: https://raw.githubusercontent.com/adafruit/Adafruit_CircuitPython_Bundle/main/badges/adafruit_discord.svg
    :target: https://adafru.it/discord
    :alt: Discord

.. image:: https://github.com/adafruit/Adafruit_CircuitPython_HX8357/workflows/Build%20CI/badge.svg
    :target: https://github.com/adafruit/Adafruit_CircuitPython_HX8357/actions/
    :alt: Build Status

.. image:: https://img.shields.io/badge/code%20style-black-000000.svg
    :target: https://github.com/psf/black
    :alt: Code Style: Black

displayio Driver for HX8357 Displays such as the 3.5-inch TFT FeatherWing and Breakout


Dependencies
=============
This driver depends on:

* `Adafruit CircuitPython <https://github.com/adafruit/circuitpython>`_

Please ensure all dependencies are available on the CircuitPython filesystem.
This is easily achieved by downloading
`the Adafruit library and driver bundle <https://github.com/adafruit/Adafruit_CircuitPython_Bundle>`_.

Usage Example
=============

.. code-block:: python

    import board
    import displayio

    # Compatibility with both CircuitPython 8.x.x and 9.x.x.
    # Remove after 8.x.x is no longer a supported release.
    try:
        from fourwire import FourWire
    except ImportError:
        from displayio import FourWire

    from adafruit_hx8357 import HX8357

    spi = board.SPI()
    tft_cs = board.D9
    tft_dc = board.D10

    displayio.release_displays()
    display_bus = FourWire(spi, command=tft_dc, chip_select=tft_cs)

    display = HX8357(display_bus, width=480, height=320)

    # Make the display context
    splash = displayio.Group()
    display.show(splash)

    color_bitmap = displayio.Bitmap(480, 320, 1)
    color_palette = displayio.Palette(1)
    color_palette[0] = 0xFF0000

    bg_sprite = displayio.TileGrid(color_bitmap,
                                   pixel_shader=color_palette,
                                   x=0, y=0)
    splash.append(bg_sprite)

    while True:
        pass

Documentation
=============

API documentation for this library can be found on `Read the Docs <https://docs.circuitpython.org/projects/hx8357/en/latest/>`_.

For information on building library documentation, please check out `this guide <https://learn.adafruit.com/creating-and-sharing-a-circuitpython-library/sharing-our-docs-on-readthedocs#sphinx-5-1>`_.

Contributing
============

Contributions are welcome! Please read our `Code of Conduct
<https://github.com/adafruit/Adafruit_CircuitPython_HX8357/blob/main/CODE_OF_CONDUCT.md>`_
before contributing to help this project stay welcoming.
