# Passwall2 Installation 

### Phase 1: Preparation

#### Step 1: Check System Architecture
Before downloading files, you need to know your router's architecture (e.g., `aarch64_cortex-a53`, `mips_24kc`).

1.  Log in to the Web Interface.
2.  Navigate to **System → Software**.
3.  Click **Update lists** to refresh the package database.

<img src="https://github.com/user-attachments/assets/48e57145-81df-47d1-b0bc-f3ddc07059b7" />

#### Step 2: Download Packages
1.  Visit the [Passwall2 Releases Page](https://github.com/xiaorouji/openwrt-passwall2/releases).
2.  Download the following files:
    *   `luci-app-passwall2_all.ipk`
    *   `passwall_packages_ipk` zip file matching your **architecture** (found in Step 1).
3.  **Unzip** the `passwall_packages` archive on your computer. You will need the files inside it for Step 4.

<img src="https://github.com/user-attachments/assets/9d93c3cf-a0c4-4d2f-8e69-93f449627a72" />

---

### Phase 2: System Configuration (SSH)

> [!WARNING]
> This step involves removing `dnsmasq` and deleting DHCP configurations. This may temporarily disrupt your network or require you to reconfigure DHCP settings later. Proceed with caution.

1.  **Connect to the router** via SSH using cmd:
    ```sh
    ssh root@192.168.1.1
    ```

2.  **Update the package repositories**:
    ```sh
    opkg update
    ```

3.  **Swap dnsmasq for dnsmasq-full**:
    Remove the default version and clean up the config:
    ```sh
    opkg remove dnsmasq
    ```
    ```sh
    rm -rf /etc/config/dhcp
    ```
4.  **Install dependencies**:
    Install the full version of dnsmasq and required kernel modules:
    ```sh
    opkg install dnsmasq-full kmod-nft-socket kmod-nft-tproxy kmod-nft-nat
    ```

---

### Phase 3: Package Installation (Web Interface)

#### Step 1: Install Core Components
1.  Go to **System → Software**.
2.  Click the **Upload Package** button.
3.  Locate the folder where you unzipped the `passwall_packages` archive.
4.  Upload and install the following packages one by one (Xray-core first is recommended):
    *   `xray-core`
    *   `v2ray-geoip`
    *   `v2ray-geosite`
    *   `tcping`
    *   `geoview`
    *   *(Optional)* Install any other packages from the folder if you specifically need them.

#### Step 2: Install the Interface (LuCI)
1.  Click **Upload Package** again.
2.  Select the `luci-app-passwall2_all.ipk` file you downloaded earlier.
3.  Install it.
