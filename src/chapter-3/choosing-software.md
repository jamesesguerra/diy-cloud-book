# Choosing your software

Before you even think about apps, services, or Docker containers, you’ll need to pick the foundation your setup will run on: the operating system (OS). For self-hosting, the clear winner is Linux, it’s the backbone of most servers worldwide, and for good reason.

## Why Linux is the Go-To for Self-Hosting
I won’t provide an exhaustive list here (a quick Google search will give you a lot more supportive arguments to back me up on this). Instead, I’ll just highlight the key reasons why Linux is the best choice. 
- **Lightweight and efficient**  
    Unlike Windows, Linux doesn’t hog resources just to stay running. This means more CPU and RAM are available for the services you actually want to host.

- **Stability**  
    Linux servers can run for months (even years) without rebooting, making it ideal for services you want always online.

- **Security**  
    Linux has a strong track record of security and benefits from frequent updates. Plus, its open-source nature means vulnerabilities are patched quickly by the community.

- **Ecosystem support**  
    Almost every self-hosted app, Docker image, or open-source project assumes you’re running Linux. Documentation, tutorials, and troubleshooting guides almost always target Linux first.

### Why Debian or Ubuntu
When it comes to self-hosting, you don’t need to look far: [Debian](https://www.debian.org/) and [Ubuntu](https://ubuntu.com/) are the most popular choices. They’re beginner-friendly, well-documented, and widely supported across hosting guides, tutorials, and community forums. So if you have 0 experience with Linux, Debian / Ubuntu is the perfect start.

- **Debian:** Known for rock-solid stability. Updates are conservative, so you’ll trade slightly older software for fewer surprises and maximum reliability. If you want a “set it and forget it” system, Debian is a safe bet.

- **Ubuntu:** Built on Debian but geared toward user-friendliness. It comes with newer software, better hardware support out of the box, and huge amounts of community documentation. If you’re new to Linux or just want something that “just works,” Ubuntu is hard to beat.

Throughout this book, assume that we're working with a Debian/Ubuntu system. This is because the most servers and tutorials use some Debian-based distro, and the Linux distro I installed on my mini PC is [Linux Mint](https://linuxmint.com/), another beginner-friendly distro built on Ubuntu. If your distro is based on RHEL, you can always look up the equivalent commands / guides, especially since package management and GPG key handling differ.

### Alternatives (for Advanced Users)

While Debian and Ubuntu are the best place to start, other Linux distributions might catch your interest later:

- **Fedora** – Bleeding-edge, with very up-to-date software. Great if you like having the latest tools, but it requires more maintenance.

- **Arch Linux** – Minimalist and highly customizable. Perfect for power users who want to learn Linux inside out, but not beginner-friendly.

- **Kali Linux** – Tailored for cybersecurity professionals and penetration testers. It comes preloaded with hundreds of security tools, making it great for hacking and security research, but it’s not designed for general self-hosting or daily use.

If you’re just starting, don’t overthink it. Stick with Debian or Ubuntu for now. You can always explore the others once you’re comfortable.

## Installing Linux
My mini PC came with Windows 10 pre-installed, which is usually the case with most used mini PCs you’ll find online. If you’ve got a mini PC as well, you can follow the same process I did:
1. Download the Linux Mint ISO (or Ubuntu/Debian if you prefer).
2. Use Balena Etcher to flash the ISO to a USB drive.
3. Plug in the USB, reboot your mini PC, and open the BIOS/boot menu.
4. Select the USB drive to boot from and begin the Linux installation.

There are many guides online if you don't wanna follow my cryptic instructions (please don't). The one I followed was [this guide](https://www.youtube.com/watch?v=_Ua-d9OeUOg) by Linus Tech Tips.

**NOTE:** Installing Linux will erase everything currently on your Windows drive (unless you explicitly set up dual boot). If you want to keep Windows around, make sure you know how to partition your drive properly.

If you’re using a VM instead of a mini PC, the process is even easier, most cloud platforms let you pick a Debian or Ubuntu ISO right from the setup wizard. It’s usually one of the first options available.