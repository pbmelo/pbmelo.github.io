---
layout: post
title:  "Creating beautiful molecular visualizations with Blender and Avogadro"
date:   2023-08-12 11:00:00 -0700
author: pedro
banner:
  image: /assets/images/render/morphine2-4k.png
categories: tutorials
tags: blender avogadro science
---

In this short tutorial, I will be showing how to render beautiful molecular visualizations (like the image below) for your presentation, website, journal cover, or just a custom artistic wallpaper using two very powerful tools, Blender and Avogadro.

![Morphine molecule render](/assets/images/render/morphine2-4k.png)

## Installing dependencies (Avogadro)

Basically, for this project we will need Avogadro and Blender, which are two software with a very simple installation process.  To optimize structures, we will need [Open Babel][open-babel].

# Debian-based (Debian, Ubuntu, Mint)
<details>
	<summary>(Click to expand)</summary>
<p>

On Debian, the command below will install Avogadro2 and its dependencies, as well as Open Babel.  It's truly straightforward.

```console
sudo apt install avogadro openbabel
```

Debian is adopting [PEP 668 – Marking Python base environments as ``externally managed''](https://peps.python.org/pep-0668/).
```console
python3 -m venv .venv
source .venv/bin/activate
```

</p>
</details>

<br>

# Arch-based (Arch, Manjaro)
<details>
	<summary>(Click to expand)</summary>
<p>

To get openbabel, simply type
```console
sudo pacman -Sy openbabel
```

But as of today, Avogadro is not available through the official Arch repositories, so you might have to install it from source, using a third party package manager like flatpak, or through the AUR.  The instructions if you're using flatpak are detailed below, while here I will explain how to get it through the AUR.

(App image)
```console
git clone https://aur.archlinux.org/avogadro2-appimage.git
cd avogadro2-appimage
makepkg -Si
makepkg -si
```

(Upstream git)
```console
git clone https://aur.archlinux.org/avogadroapp.git
cd avogadro2-appimage
makepkg -Si
makepkg -si
```

</p>
</details>

<br>

# Fedora-based (Fedora)
<details>
	<summary>(Click to expand)</summary>
<p>

```console
sudo rpm install avogadro2 openbabel
```

</p>
</details>

<br>

# Flatpak
<details>
	<summary>(Click to expand)</summary>
<p>

```console
sudo flatpak install flathub org.openchemistry.Avogadro2
```

</p>
</details>

<br>

# AppImages from GitHub or building from source.
<details>
	<summary>(Click to expand)</summary>
<p>

[The official OpenChemistry GitHub repository for avogadro][avogadro-libs] provides nightly AppImage builds that you can download straight through your browser.  Alternatively, they provide detailed instructions on how to build it from souce [here](https://two.avogadro.cc/install/build.html).

</p>
</details>

#### Comment about Blender
I recommend using Blender AppImage instead of installing it from some distribution repository.  I am generally in favor of using your own distro's repositories whenever possible, with a few exceptions.  Generally, software that is being constantly updated will tend to have compatibility issues when opening your project files across machines with different versions installed.  Usually, this is not a big deal, but since Blender is so complex to the point where you will be looking up tutorials all the time and its community is so active, it's good to have an updated version so you can follow current trends.

You can download the AppImage directly from [Blender's website][blender] ([https://www.blender.org/download/](https://www.blender.org/download/)).

After installing Blender, we will need the Atomic Blender addon.  You can get it by clicking on Edit, Preferences, Add-ons, search for "[Atomic Blender][atomic-blender]", then click install.  After this, you can close the window.  Now, after going to File, Import, a "Protein Data Bank (.pdb)" option will be available.  Click on it, and a new pop-up window will appear, where you can import pdb files.

## Building molecular structure, from a database or building manually
If you can get your molecular structure from a database such as [PubChem][pubchem], or simply have a SMILES or International Chemical Identifier (InChI) code, you can build it to Avogadro in a straightforward way.  On Avogadro's main screen, simply click Build, Insert, then the format that you want to import.  A pop-up window will appear, where you can paste the molecule identifier, and click OK.

A new pop-up window "Building the Molecule" with a loading bar will show up.  When loading is complete, you will see the 3D structure your molecule.

For example, I went to [the Wikipedia page for morphine][wiki-morphine] (a beautiful, small yet complex molecule, presenting non-planar rings and chiral centers) and got it's SMILES code, which is `CN1CC[C@]23C4=C5C=CC(O)=C4O[C@H]2[C@@H](O)C=C[C@H]3[C@H]1C5`, and followed the instructions above.

Alternatively, you can simply add atoms and bonds one by one.  This might be better for simple compounds, but cumbersome for more complicated structures.

### Optimizing structures
After you have your molecular structure, click Extensions -> OpenBabel -> Optimize Geometry (`Ctrl+Alt+O`), and your structure will optimized, using a mathematical model to calculate the separation and angles between atoms and bonds.

## Importing structure to Blender
After you are happy with your geometry optimization, export your molecule with File -> Export -> Molecule, and save it with a `.pdb` extension.

Now you can open Blender, and under File -> Import Protein Databank (.pdb), find your `.pdb` file.  You will notice that your molecule will appear as imported.  Now it's time to use your creativity to add shaders, lights, a nice background to your render, and play with camera angles.

## Shaders, lighting, background, camera

For this specific render, I will follow a safe procedure that I came up with when I first started rendering molecules, consisting of:

1. Setting the materials of the atoms/bonds to a glass shader;
2. Adding a base, "floor" plane, shaded as a slightly glossy, reflective material;
3. Inserting two or three light sources, preferably of an interesting shape;
4. Duplicating the molecule around the scene to create interesting reflections and a catching background;
5. Set camera's position and a depth of field to create a more artistic effect.

## Useful links and references

1. [Open Babel][open-babel]
2. [Avogadro libs][avogadro-libs]
3. [Blender][blender]
4. [Atomic Blender][atomic-blender]
5. [PubChem][pubchem]
6. [Morphine on Wikipedia][wiki-morphine]

[open-babel]: https://www.openbabel.org/
[avogadro-libs]: https://github.com/OpenChemistry/avogadrolibs
[blender]: https://www.blender.org/download/
[atomic-blender]: https://docs.blender.org/manual/en/latest/addons/import_export/mesh_atomic.html
[pubchem]: https://pubchem.ncbi.nlm.nih.gov/
[wiki-morphine]: https://en.wikipedia.org/wiki/Morphine