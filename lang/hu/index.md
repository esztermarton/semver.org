---
title: Semantic Versioning 2.0.0
redirect_from: /lang/hu/
---

Semantic Versioning 2.0.0
==============================

Összefoglalás
-------

Vegyünk egy adott verzió számot, MAJOR.MINOR.PATCH, és növeljük:

1. a MAJOR verzió számot ha a változtatásaink eredményeként elveszítjük a
   kompatibilitást korábbi verziókkal
2. a MINOR verzió számot ha olyan funkcionalitásokat adunk amik megőrzik a
hátrafele kompatibilitást.
3. a PATCH verzió számot ha hátrafele kompatibilis hiba-javításokat adunk hozzá?.

További RELEASE? előtti címkéket és BUILD? metaadatokat a MAJOR.MINOR.PATCH
formátum kiegészítéseként lehet még hozzáadni.

Bevezető
------------

A szoftver menedzsment univerzumában létezik egy hely, ami még a bátrak szívét
is megrendíti: az Ôsszefüggések Számontartásának Pokolja. Minél nagyobbra nő a
rendszered, minél több csomagot adsz hozzá, annál valószínűbb hogy előbb
utóbb ebben az átkozott zúgban találod magad.

Sok összefüggésekkel rendelkező rendszerekben az új csomagverziók hozzáadása
gyorsan rémálommá alakul át. Ha túl szigorúak az szoftver-függéseidnek a leírásai,
fenn áll a veszélye annak, hogy "version lock" alakul ki (amikor nem tudsz úgy
frissíteni egy csomagot, hogy vele együtt az összes tőle függő csomgagot ne
frissítsd). Ugyanakkor, ha túl szabadon vannak ugyanezek megszabva,
elkerülhetetlen, hogy idővel utólérjen a verzió-PROMISCUITY? (amikor jobb
kompatibilitást remélünk szoftver komponensek között mint ami realisztikus).
Az Ôsszefüggések Számontartásának Pokolja az, amikor e két helyzet közül az
egyik vagy akár egyszerre mindkettő meggátol a projekt könnyed és rizikómentes
előrevitelében.

Erre a problémára válaszként fejlesztettem ki az itt található szabály- és
feltételrendszert amik meghatározza, hogy hogyan válasszuk és növeljük a
verziószámokat. A szabályok alapja - bár nem egyetlen forrása - már elterjedt,
jólműködő PRACTICES?? amik egyaránt találhatóak CLOSED és open-source
szoftverben. Az rendszer első feltétele egy publikus API létrehozása: ez
egyaránt lehet dokumentáció formájában, vagy a programon keresztül meghatározva.
Kulcsfontosságú, hogy ez az API átlátható es precíz?? legyen. Amiután az API már
közzé lett téve, minden változást a szoftverben verziószám növelésével
kommunikálunk. A X.Y.Z (Major.Minor.Patch) formátumot választjuk. Hiba javítások
amik nem érintik az API-t a "patch" verziószámot; hátrafele kompatibilis
fejlesztések a "minor" verziószámot; kompatibilitást megszakító változások a
"major" verziószámot növelik.

A rendszert "Semantic Versioning", tehát szemantikus verziószámozásnak
kereszteltem. A séma mellett a szoftver evolúcióját az őt fedő verziószámok
változása tükrözi: a verziószámok így valós jelentéssel bírnak.


A szemantikus verziószámozás leírása (SemVer)
------------------------------------------

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](http://tools.ietf.org/html/rfc2119).

1. Szemantikus verziózást használó szoftvernek MUSZÁJ publikus API-t közzétenni.
Ez az felület létezhet kizárolag dokumentáció formájában, vagy akár szoftverben
meghatározva, de mindenféleképpen szükséges, hogy precíz és COMPREHENSIVE legyen.

2. Az általános verziószám formátuma MUSZÁJ, hogy az X.Y.Z legyen, ahol az X, Y
és Z a természetes számok halmazába tartoznak, kezdő nullák nélkül. X a
"major", Y a "minor" és Z a "patch" verziószám. Mindhárom MUSZÁJ, hogy
számtanilag helyesen növekedjen. Például: 1.9.0 -> 1.10.0 -> 1.11.0.

3. Amint egy verziózott csomag RELEASE-elve?? lett, a csomag tartalma nem
változhat. Bármilyen változás MUSZÁJ, hogy új verzióként legyen hozzáadva.

4. A nulladik "major" verzió (0.Y.Z) korai fejlesztésekre alkalmazható. Bárhol
várhatóak változások a szoftverben és a publikus API-tól nem elvárható, hogy
tökéletesen stabil legyen.

5. Az első verzió (1.0.0) defíniálja a publikus API-t. Ezt követő
verziószámok ennek az API-nak a változásától függnek.

6. A "patch", Z verziószámot (x.y.Z | x > 0) MUSZÁJ növelni, amikor kizárólag
hátrafele kompatibilis hibajavításokat addunk a szoftverhez. Ilyen "bug-fix"
definiciója?? egy olyan belső változás ami addig hibás viselkedést korrigál.

7. A "minor", Y verziószámot (x.Y.z | x > 0) MUSZÁJ növelni, amikor olyan új
funkciókat adunk hozzá az API-hoz, ami a hátrafele kompatibilitást nem érinti.
MUSZÁJ növelni, amikor korábbi funkciókat megjelölünk mint DEPRECATED?. Növelni
LEHET, amikor a új funkciók kerülnek a belső, privát kódbázisba. TartalmazHAT
"patch" szintű változásokat is. A "patch" verziószám MUSZÁJ, hogy nullára
csökkenjen amikor a "minor" verziószám növekszik

7. Minor version Y (x.Y.z | x > 0) MUST be incremented if new, backwards
compatible functionality is introduced to the public API. It MUST be
incremented if any public API functionality is marked as deprecated. It MAY be
incremented if substantial new functionality or improvements are introduced
within the private code. It MAY include patch level changes. Patch version
MUST be reset to 0 when minor version is incremented.

8. Major version X (X.y.z | X > 0) MUST be incremented if any backwards
incompatible changes are introduced to the public API. It MAY include minor
and patch level changes. Patch and minor version MUST be reset to 0 when major
version is incremented.

9. A pre-release version MAY be denoted by appending a hyphen and a
series of dot separated identifiers immediately following the patch
version. Identifiers MUST comprise only ASCII alphanumerics and hyphen
[0-9A-Za-z-]. Identifiers MUST NOT be empty. Numeric identifiers MUST
NOT include leading zeroes. Pre-release versions have a lower
precedence than the associated normal version. A pre-release version
indicates that the version is unstable and might not satisfy the
intended compatibility requirements as denoted by its associated
normal version. Examples: 1.0.0-alpha, 1.0.0-alpha.1, 1.0.0-0.3.7,
1.0.0-x.7.z.92.

10. Build metadata MAY be denoted by appending a plus sign and a series of dot
separated identifiers immediately following the patch or pre-release version.
Identifiers MUST comprise only ASCII alphanumerics and hyphen [0-9A-Za-z-].
Identifiers MUST NOT be empty. Build metadata SHOULD be ignored when determining
version precedence. Thus two versions that differ only in the build metadata,
have the same precedence. Examples: 1.0.0-alpha+001, 1.0.0+20130313144700,
1.0.0-beta+exp.sha.5114f85.

11. Precedence refers to how versions are compared to each other when ordered.
Precedence MUST be calculated by separating the version into major, minor, patch
and pre-release identifiers in that order (Build metadata does not figure
into precedence). Precedence is determined by the first difference when
comparing each of these identifiers from left to right as follows: Major, minor,
and patch versions are always compared numerically. Example: 1.0.0 < 2.0.0 <
2.1.0 < 2.1.1. When major, minor, and patch are equal, a pre-release version has
lower precedence than a normal version. Example: 1.0.0-alpha < 1.0.0. Precedence
for two pre-release versions with the same major, minor, and patch version MUST
be determined by comparing each dot separated identifier from left to right
until a difference is found as follows: identifiers consisting of only digits
are compared numerically and identifiers with letters or hyphens are compared
lexically in ASCII sort order. Numeric identifiers always have lower precedence
than non-numeric identifiers. A larger set of pre-release fields has a higher
precedence than a smaller set, if all of the preceding identifiers are equal.
Example: 1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-alpha.beta < 1.0.0-beta <
1.0.0-beta.2 < 1.0.0-beta.11 < 1.0.0-rc.1 < 1.0.0.

Why Use Semantic Versioning?
----------------------------

This is not a new or revolutionary idea. In fact, you probably do something
close to this already. The problem is that "close" isn't good enough. Without
compliance to some sort of formal specification, version numbers are
essentially useless for dependency management. By giving a name and clear
definition to the above ideas, it becomes easy to communicate your intentions
to the users of your software. Once these intentions are clear, flexible (but
not too flexible) dependency specifications can finally be made.

A simple example will demonstrate how Semantic Versioning can make dependency
hell a thing of the past. Consider a library called "Firetruck." It requires a
Semantically Versioned package named "Ladder." At the time that Firetruck is
created, Ladder is at version 3.1.0. Since Firetruck uses some functionality
that was first introduced in 3.1.0, you can safely specify the Ladder
dependency as greater than or equal to 3.1.0 but less than 4.0.0. Now, when
Ladder version 3.1.1 and 3.2.0 become available, you can release them to your
package management system and know that they will be compatible with existing
dependent software.

As a responsible developer you will, of course, want to verify that any
package upgrades function as advertised. The real world is a messy place;
there's nothing we can do about that but be vigilant. What you can do is let
Semantic Versioning provide you with a sane way to release and upgrade
packages without having to roll new versions of dependent packages, saving you
time and hassle.

If all of this sounds desirable, all you need to do to start using Semantic
Versioning is to declare that you are doing so and then follow the rules. Link
to this website from your README so others know the rules and can benefit from
them.


FAQ
---

### How should I deal with revisions in the 0.y.z initial development phase?

The simplest thing to do is start your initial development release at 0.1.0
and then increment the minor version for each subsequent release.

### How do I know when to release 1.0.0?

If your software is being used in production, it should probably already be
1.0.0. If you have a stable API on which users have come to depend, you should
be 1.0.0. If you're worrying a lot about backwards compatibility, you should
probably already be 1.0.0.

### Doesn't this discourage rapid development and fast iteration?

Major version zero is all about rapid development. If you're changing the API
every day you should either still be in version 0.y.z or on a separate
development branch working on the next major version.

### If even the tiniest backwards incompatible changes to the public API require a major version bump, won't I end up at version 42.0.0 very rapidly?

This is a question of responsible development and foresight. Incompatible
changes should not be introduced lightly to software that has a lot of
dependent code. The cost that must be incurred to upgrade can be significant.
Having to bump major versions to release incompatible changes means you'll
think through the impact of your changes, and evaluate the cost/benefit ratio
involved.

### Documenting the entire public API is too much work!

It is your responsibility as a professional developer to properly document
software that is intended for use by others. Managing software complexity is a
hugely important part of keeping a project efficient, and that's hard to do if
nobody knows how to use your software, or what methods are safe to call. In
the long run, Semantic Versioning, and the insistence on a well defined public
API can keep everyone and everything running smoothly.

### What do I do if I accidentally release a backwards incompatible change as a minor version?

As soon as you realize that you've broken the Semantic Versioning spec, fix
the problem and release a new minor version that corrects the problem and
restores backwards compatibility. Even under this circumstance, it is
unacceptable to modify versioned releases. If it's appropriate,
document the offending version and inform your users of the problem so that
they are aware of the offending version.

### What should I do if I update my own dependencies without changing the public API?

That would be considered compatible since it does not affect the public API.
Software that explicitly depends on the same dependencies as your package
should have their own dependency specifications and the author will notice any
conflicts. Determining whether the change is a patch level or minor level
modification depends on whether you updated your dependencies in order to fix
a bug or introduce new functionality. I would usually expect additional code
for the latter instance, in which case it's obviously a minor level increment.

### What if I inadvertently alter the public API in a way that is not compliant with the version number change (i.e. the code incorrectly introduces a major breaking change in a patch release)?

Use your best judgment. If you have a huge audience that will be drastically
impacted by changing the behavior back to what the public API intended, then
it may be best to perform a major version release, even though the fix could
strictly be considered a patch release. Remember, Semantic Versioning is all
about conveying meaning by how the version number changes. If these changes
are important to your users, use the version number to inform them.

### Hogyan kezeljem az elavult funkcionalitást?

Teljesen normális esemény a szoftverfejlesztésben, hogy egyes funkcionalitások elavulnak, sőtt mi több, gyakran elvárt a szoftver fejlődésének érdekében. Amikor lecserélsz egy elavult részt a publikus API-dban, két dolgot kell tenned: (1) frissítsd a dokumentációt, hogy a felhasználók tudjanak a változásról, (2) eszközölj egy új minor kiadást az elavult résszel. Mielőtt teljesen eltörölnéd a funkcionalitást egy új, major kiadásban, kell lennie egy minor kiadásnak ami még tartalmazza az elavult részt, hogy a felhasználók zökkenőmentesen áttudjanak állni az új API-ra. 

### Vannak-e megszorítások a verzió string hosszára nézve a semver szerint?

Nincs, de becsüljük meg ésszerűen a hosszát. Például, egy 255 karakteres verzió string erős túlzás. Különböző 
rendszereknél, különböző verzió string hossz korlátokat alkalmazhatnak.

About
-----

The Semantic Versioning specification is authored by [Tom
Preston-Werner](http://tom.preston-werner.com), inventor of Gravatars and
cofounder of GitHub.

If you'd like to leave feedback, please [open an issue on
GitHub](https://github.com/mojombo/semver/issues).


License
-------

[Creative Commons - CC BY 3.0](http://creativecommons.org/licenses/by/3.0/)
