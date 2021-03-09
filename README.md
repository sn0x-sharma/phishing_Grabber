# PhishingGrabber

PhishingGrabberpossible phishing domains in near real time by looking for suspicious TLS certificate issuances reported to the [Certificate Transparency Log (CTL)](https://www.certificate-transparency.org/) via the [CertStream](https://certstream.calidog.io/) API. "Suspicious" issuances are those whose domain name scores beyond a certain threshold based on a configuration file.

This is just a working PoC. Feel free to contribute and tweak the code to fit your needs. 👍



### Installation

The script should work fine using Python2 or Python3. In either case, install the requirements after cloning or downloading the source code:

```sh
pip install -r requirements.txt
```

### Configuration

PhishingGrabber uses a simple YAML configuration file to assign a numeric score for strings that can be found in a TLS certificate's common name or SAN field (i.e., a cert's domain name). The configuration file, [`suspicious.yaml`](suspicious.yaml), ships with sensible defaults, but you can adjust or add to both the strings it contains and the score assigned to each string by editing an override file, [`external.yaml`](external.yaml).

Both the default `suspicious.yaml` and the user-modifiable `external.yaml` configuration files contain two YAML dictionaries: `keywords` and `tlds`. The keys of the dictionaries are the strings and the values are the scores to assign if that string is found in the domain name for an issued certificate. For example:

```yaml
keywords:
    'login': 25
```

Here, a score of `25` is added to the generic keyword `login` when it is found in a TLS certificate domain name. Increasing this value will raise the level of suspicion against domains with the string `login` in them, thus allowing you to subject these certificate issuances to increased scrutiny.

However, in order to be reported as suspicious by PhishingGrabber, the score assigned to a given certificate must meet or exceed (`>=`, "greater than or equal to") the following thresholds:

| Score | Reported as  |
| -----:| ------------ |
|    65 | `Potential`  |
|    80 | `Likely`     |
|    90 | `Suspicious` |

> :bulb: See the `score_domain()` function in the source code for details regarding the scoring algorithm.

### Usage

Once configured to your liking, usage is as simple as running the script:

```
$ ./phishing_Grabber.py
```

### Example phishing caught

![Paypal Phishing](https://i.imgur.com/AK60EYz.png)

### PhishingGrabber in Docker container

If you running MacOs or having a different OS version that would make the installation of phishing_Grabber difficult, then having the tool dockerized is one of your options.

```
docker build . -t phishing_Grabber
```

# License

GNU GPLv3

# contact
## Email : sn0x-nuxer890@protonmail.com
## instagram : _sn0x_
## Github : sn0x-sharma
## linkedin : sanket sharma


