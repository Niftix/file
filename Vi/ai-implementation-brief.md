# Brief IA — intégration visuelle complète de Vi (Base, client 4.20)

## Mission

Auditer l’implémentation existante de `Vi`, puis relier correctement ses animations, particules, os d’attache et événements temporels. Préserver la logique de gameplay déjà fonctionnelle : ce brief n’autorise pas une réécriture de l’architecture ou du netcode.

## Règles impératives

1. Lire le code existant avant toute modification et identifier les API déjà utilisées pour animation, particules, buffs, missiles et réplication.
2. Ne pas importer ni republier les ressources binaires Riot. Référencer uniquement leurs noms internes déjà présents dans le client 4.20 local.
3. Une preuve `high` peut être appliquée directement après vérification du flux réseau. Une preuve `medium` doit être confirmée en jeu. Une candidate `low` ne doit jamais être activée uniquement à cause de son nom.
4. Ne pas confondre animation du lanceur, animation de la cible, particule de missile et particule d’impact.
5. Toute particule persistante doit avoir un propriétaire, un os d’attache, une durée de vie et un chemin explicite de suppression.
6. Ne jamais relancer une animation d’apparition ou de début lorsque l’entité redevient simplement visible.
7. Conserver les identifiants et la casse du client dans les données ; faire les comparaisons de résolution sans tenir compte de la casse.
8. Produire des tests automatisés et une procédure de vérification en jeu pour chaque phase.

## Livrables attendus

- tableau des hooks existants et des hooks ajoutés ;
- implémentation séparant `cast`, `channel/loop`, `release/movement`, `impact` et `winddown` ;
- nettoyage déterministe des effets lors d’une interruption, mort, désactivation ou fin de sort ;
- tests unitaires des séquences et tests d’intégration des événements envoyés au client ;
- compte rendu des preuves utilisées et des candidats rejetés.

## Contrat extrait par sort

### Q

Sous-objets liés : `root`, `vipassivebuff`, `viq`, `viqanimations`, `viqdash`, `viqknockback`, `viqlaunch`, `viqlaunchsound`, `viqmarker`, `viqminion`, `viqminionhit`, `viqrefresh`, `viqvfx`, `viw`, `viwbuff`, `viwproc`, `viwshred`, `viwvisual`

Séquence :

- `cast` — INIBIN animation/timing — confiance `high`.
- `channel_or_loop` — preload/ANM naming — confiance `medium`.
- `movement_or_missile` — dependent spell graph — confiance `medium`.
- `impact` — INIBIN/dependent spell — confiance `high`.
- `winddown` — INIBIN animation — confiance `high`.

Temporalité :

- `cast_event_seconds` = `0.25`
- `cast_event_basis` = `SpellData.CastFrame / Vi_Spell1 fps`
- `confidence` = `high`
- `channel_duration_seconds` = `1.25`

Animations :

- `Vi_Spell1` — `1.6667 s`, `30.0 fps` — confiance `high` — source `Skins/Base/Animations/Vi_Spell1.anm`.
- `Vi_Spell1_Idle` — `0.9032 s`, `31.0 fps` — confiance `high` — source `Skins/Base/Animations/Vi_Spell1_Idle.anm`.
- `Vi_SPELL1_IdleIntro` — `2.0 s`, `30.0 fps` — confiance `high` — source `Skins/Base/Animations/Vi_SPELL1_IdleIntro.anm`.
- `Vi_Spell1_Run` — `1.2333 s`, `30.0 fps` — confiance `high` — source `Skins/Base/Animations/Vi_Spell1_Run.anm`.
- `Vi_Spell3` — `1.7 s`, `30.0 fps` — confiance `medium` — source `Skins/Base/Animations/Vi_Spell3.anm`.

Particules prouvées par les PRELOAD/INIBIN :

- `vi_armorshred.troy` → `Skins/Base/Particles/Vi_ArmorShred.troybin` — confiance `high` — portée `selected_skin`.
- `vi_armorshred_dragon.troy` → `Skins/Base/Particles/VI_ArmorShred_Dragon.troybin` — confiance `high` — portée `selected_skin`.
- `vi_armorshred_hit_1.troy` → `Skins/Base/Particles/Vi_ArmorShred_Hit_1.troybin` — confiance `high` — portée `selected_skin`.
- `vi_armorshred_hit_2.troy` → `Skins/Base/Particles/Vi_ArmorShred_Hit_2.troybin` — confiance `high` — portée `selected_skin`.
- `vi_armorshred_hit_minion_1.troy` → `Skins/Base/Particles/Vi_ArmorShred_Hit_Minion_1.troybin` — confiance `high` — portée `selected_skin`.
- `vi_armorshred_hit_minion_2.troy` → `Skins/Base/Particles/Vi_ArmorShred_Hit_Minion_2.troybin` — confiance `high` — portée `selected_skin`.
- `vi_armorshred_hold.troy` → `Skins/Base/Particles/Vi_ArmorShred_hold.troybin` — confiance `high` — portée `selected_skin`.
- `vi_armorshred_minion.troy` → `Skins/Base/Particles/Vi_ArmorShred_Minion.troybin` — confiance `high` — portée `selected_skin`.
- `vi_attack_speed_buff.troy` → `Skins/Base/Particles/Vi_Attack_Speed_Buff.troybin` — confiance `high` — portée `selected_skin`.
- `vi_e_attackspeed_knuckles.troy` → `Skins/Base/Particles/VI_E_AttackSpeed_Knuckles.troybin` — confiance `high` — portée `selected_skin`.
- `vi_passive_buff.troy` → `Skins/Base/Particles/Vi_Passive_Buff.troybin` — confiance `high` — portée `selected_skin`.
- `vi_passive_buff_deactivate.troy` → `Skins/Base/Particles/Vi_Passive_Buff_DeActivate.troybin` — confiance `high` — portée `selected_skin`.
- `vi_passive_hand_l.troy` → `Skins/Base/Particles/Vi_passive_Hand_L.troybin` — confiance `high` — portée `selected_skin`.
- `vi_passive_hand_r.troy` → `Skins/Base/Particles/Vi_passive_Hand_R.troybin` — confiance `high` — portée `selected_skin`.
- `vi_passive_shield.troy` → `Skins/Base/Particles/Vi_Passive_Shield.troybin` — confiance `high` — portée `selected_skin`.
- `vi_q_channel_01.troy` → `Skins/Base/Particles/Vi_Q_Channel_01.troybin` — confiance `high` — portée `selected_skin`.
- `vi_q_channel_02.troy` → `Skins/Base/Particles/Vi_Q_Channel_02.troybin` — confiance `high` — portée `selected_skin`.
- `vi_q_channel_l.troy` → `Skins/Base/Particles/Vi_Q_Channel_L.troybin` — confiance `high` — portée `selected_skin`.
- `vi_q_expire.troy` → `Skins/Base/Particles/Vi_Q_Expire.troybin` — confiance `high` — portée `selected_skin`.
- `vi_q_minion_tar.troy` → `Skins/Base/Particles/Vi_Q_Minion_tar.troybin` — confiance `high` — portée `selected_skin`.
- `vi_q_tar.troy` → `Skins/Base/Particles/Vi_Q_tar.troybin` — confiance `high` — portée `selected_skin`.

Candidates trouvées uniquement par convention de nommage :

- `Vi_Q_Fist_Shockwave_L` — `Skins/Base/Particles/Vi_Q_Fist_Shockwave_L.troybin` — confiance `low`, validation manuelle obligatoire.
- `Vi_Q_mis` — `Skins/Base/Particles/Vi_Q_mis.troybin` — confiance `low`, validation manuelle obligatoire.
- `Vi_Q_mis_Child` — `Skins/Base/Particles/Vi_Q_mis_Child.troybin` — confiance `low`, validation manuelle obligatoire.
- `Vi_Q_Skin_Swap` — `Skins/Base/Particles/Vi_Q_Skin_Swap.troybin` — confiance `low`, validation manuelle obligatoire.

Os à valider :

- `root` — présent dans le squelette sélectionné.

### W

Sous-objets liés : `root`, `vipassivebuff`, `viw`, `viwbuff`, `viwshred`

Séquence :

- Aucune phase animée prouvée : ne pas en inventer une.

Temporalité :

- Pas de temps calculable avec certitude.

Animations :

- Aucune animation associée. Cela peut être normal pour un passif.

Particules prouvées par les PRELOAD/INIBIN :

- `vi_armorshred.troy` → `Skins/Base/Particles/Vi_ArmorShred.troybin` — confiance `high` — portée `selected_skin`.
- `vi_armorshred_dragon.troy` → `Skins/Base/Particles/VI_ArmorShred_Dragon.troybin` — confiance `high` — portée `selected_skin`.
- `vi_armorshred_hold.troy` → `Skins/Base/Particles/Vi_ArmorShred_hold.troybin` — confiance `high` — portée `selected_skin`.
- `vi_armorshred_minion.troy` → `Skins/Base/Particles/Vi_ArmorShred_Minion.troybin` — confiance `high` — portée `selected_skin`.
- `vi_attack_speed_buff.troy` → `Skins/Base/Particles/Vi_Attack_Speed_Buff.troybin` — confiance `high` — portée `selected_skin`.
- `vi_e_attackspeed_knuckles.troy` → `Skins/Base/Particles/VI_E_AttackSpeed_Knuckles.troybin` — confiance `high` — portée `selected_skin`.
- `vi_passive_buff.troy` → `Skins/Base/Particles/Vi_Passive_Buff.troybin` — confiance `high` — portée `selected_skin`.
- `vi_passive_buff_deactivate.troy` → `Skins/Base/Particles/Vi_Passive_Buff_DeActivate.troybin` — confiance `high` — portée `selected_skin`.
- `vi_passive_hand_l.troy` → `Skins/Base/Particles/Vi_passive_Hand_L.troybin` — confiance `high` — portée `selected_skin`.
- `vi_passive_hand_r.troy` → `Skins/Base/Particles/Vi_passive_Hand_R.troybin` — confiance `high` — portée `selected_skin`.
- `vi_passive_shield.troy` → `Skins/Base/Particles/Vi_Passive_Shield.troybin` — confiance `high` — portée `selected_skin`.

Candidates trouvées uniquement par convention de nommage :

- Aucune candidate supplémentaire.

Os à valider :

- `C_BUFFBONE_GLB_HEAD_LOC` — présent dans le squelette sélectionné.
- `R_hand` — présent dans le squelette sélectionné.

### E

Sous-objets liés : `root`, `vie`, `vipassivebuff`

Séquence :

- `cast` — INIBIN animation/timing — confiance `high`.
- `impact` — INIBIN/dependent spell — confiance `high`.

Temporalité :

- Pas de temps calculable avec certitude.

Animations :

- `Vi_Spell2` — `1.7 s`, `30.0 fps` — confiance `high` — source `Skins/Base/Animations/Vi_Spell2.anm`.
- `Vi_Spell2_A` — `1.7 s`, `30.0 fps` — confiance `high` — source `Skins/Base/Animations/Vi_Spell2_A.anm`.

Particules prouvées par les PRELOAD/INIBIN :

- `anniebasicattack_mis.troy` → `EXTERNE OU NON RÉSOLUE` — confiance `medium` — portée `unresolved`.
- `malphite_enrage_glow.troy` → `EXTERNE OU NON RÉSOLUE` — confiance `medium` — portée `unresolved`.
- `vi_e_activate_hands_l.troy` → `Skins/Base/Particles/Vi_E_activate_hands_L.troybin` — confiance `high` — portée `selected_skin`.
- `vi_e_activate_hands_r.troy` → `Skins/Base/Particles/Vi_E_activate_hands_R.troybin` — confiance `high` — portée `selected_skin`.
- `vi_passive_buff.troy` → `Skins/Base/Particles/Vi_Passive_Buff.troybin` — confiance `high` — portée `selected_skin`.
- `vi_passive_buff_deactivate.troy` → `Skins/Base/Particles/Vi_Passive_Buff_DeActivate.troybin` — confiance `high` — portée `selected_skin`.
- `vi_passive_hand_l.troy` → `Skins/Base/Particles/Vi_passive_Hand_L.troybin` — confiance `high` — portée `selected_skin`.
- `vi_passive_hand_r.troy` → `Skins/Base/Particles/Vi_passive_Hand_R.troybin` — confiance `high` — portée `selected_skin`.
- `vi_passive_shield.troy` → `Skins/Base/Particles/Vi_Passive_Shield.troybin` — confiance `high` — portée `selected_skin`.

Candidates trouvées uniquement par convention de nommage :

- `Vi_E_activate_hands` — `Skins/Base/Particles/Vi_E_activate_hands.troybin` — confiance `low`, validation manuelle obligatoire.
- `VI_E_AttackSpeed_Knuckles` — `Skins/Base/Particles/VI_E_AttackSpeed_Knuckles.troybin` — confiance `low`, validation manuelle obligatoire.
- `Vi_E_Cas` — `Skins/Base/Particles/Vi_E_Cas.troybin` — confiance `low`, validation manuelle obligatoire.
- `Vi_E_Minion_tar` — `Skins/Base/Particles/Vi_E_Minion_tar.troybin` — confiance `low`, validation manuelle obligatoire.
- `Vi_E_Shockwave_Child` — `Skins/Base/Particles/Vi_E_Shockwave_Child.troybin` — confiance `low`, validation manuelle obligatoire.
- `Vi_E_Shockwave_tar` — `Skins/Base/Particles/Vi_E_Shockwave_tar.troybin` — confiance `low`, validation manuelle obligatoire.
- `Vi_E_tar` — `Skins/Base/Particles/Vi_E_tar.troybin` — confiance `low`, validation manuelle obligatoire.

Os à valider :

- `R_hand` — présent dans le squelette sélectionné.
- `root` — présent dans le squelette sélectionné.

### R

Sous-objets liés : `expirationtimer`, `suppression`, `unstoppableforcemarker`, `vir`, `virdunk`, `virdunkghost`, `virdunkmarker`, `virdunkring`, `virdunkstun`, `virdunktarget`, `virdunktargetself`, `virdunkvfx`, `virhit`, `virknockback`, `virtarget`, `virtracker`, `virvoice`, `viteamwork`

Séquence :

- `cast` — INIBIN animation/timing — confiance `high`.
- `impact` — INIBIN/dependent spell — confiance `high`.

Temporalité :

- `cast_event_seconds` = `0.25`
- `cast_event_basis` = `SpellData.OverrideCastTime`
- `confidence` = `high`

Animations :

- `Vi_Spell2` — `1.7 s`, `30.0 fps` — confiance `medium` — source `Skins/Base/Animations/Vi_Spell2.anm`.
- `Vi_Spell2_A` — `1.7 s`, `30.0 fps` — confiance `medium` — source `Skins/Base/Animations/Vi_Spell2_A.anm`.
- `Vi_Spell4` — `0.6452 s`, `31.0 fps` — confiance `high` — source `Skins/Base/Animations/Vi_Spell4.anm`.
- `Vi_Spell4_hit` — `0.9355 s`, `31.0 fps` — confiance `high` — source `Skins/Base/Animations/Vi_Spell4_hit.anm`.
- `Vi_Spell4_run` — `1.0 s`, `31.0 fps` — confiance `high` — source `Skins/Base/Animations/Vi_Spell4_run.anm`.

Particules prouvées par les PRELOAD/INIBIN :

- `anniebasicattack_mis.troy` → `EXTERNE OU NON RÉSOLUE` — confiance `medium` — portée `unresolved`.
- `disintegrate_mis.troy` → `EXTERNE OU NON RÉSOLUE` — confiance `medium` — portée `unresolved`.
- `disintegrate_tar.troy` → `EXTERNE OU NON RÉSOLUE` — confiance `medium` — portée `unresolved`.
- `disintegratehit_tar.troy` → `EXTERNE OU NON RÉSOLUE` — confiance `medium` — portée `unresolved`.
- `headbutt_tar.troy` → `EXTERNE OU NON RÉSOLUE` — confiance `medium` — portée `unresolved`.
- `stun_glb.troy` → `EXTERNE OU NON RÉSOLUE` — confiance `medium` — portée `unresolved`.
- `vi_r_chargedrun_impact.troy` → `Skins/Base/Particles/Vi_R_ChargedRun_impact.troybin` — confiance `high` — portée `selected_skin`.
- `vi_r_dash_tar.troy` → `Skins/Base/Particles/Vi_R_Dash_tar.troybin` — confiance `high` — portée `selected_skin`.
- `vi_r_knockback_tar.troy` → `Skins/Base/Particles/Vi_R_Knockback_tar.troybin` — confiance `high` — portée `selected_skin`.
- `vi_r_laser_target.troy` → `Skins/Base/Particles/Vi_R_Laser_Target.troybin` — confiance `high` — portée `selected_skin`.
- `vi_r_pillar.troy` → `Skins/Base/Particles/Vi_R_Pillar.troybin` — confiance `high` — portée `selected_skin`.
- `vi_r_target_indicator.troy` → `Skins/Base/Particles/Vi_R_target_Indicator.troybin` — confiance `high` — portée `selected_skin`.
- `vi_r_target_indicator_02.troy` → `Skins/Base/Particles/Vi_R_target_Indicator_02.troybin` — confiance `high` — portée `selected_skin`.
- `vi_racer_r_pillar.troy` → `Skins/Skin01/Particles/Vi_Racer_R_Pillar.troybin` — confiance `medium` — portée `other_skin`.

Candidates trouvées uniquement par convention de nommage :

- `Vi_R_Cas_start` — `Skins/Base/Particles/Vi_R_Cas_start.troybin` — confiance `low`, validation manuelle obligatoire.
- `Vi_R_DunkTarget_tar` — `Skins/Base/Particles/Vi_R_DunkTarget_tar.troybin` — confiance `low`, validation manuelle obligatoire.
- `Vi_R_Fist_R` — `Skins/Base/Particles/Vi_R_Fist_R.troybin` — confiance `low`, validation manuelle obligatoire.
- `Vi_R_Indicator_Child` — `Skins/Base/Particles/Vi_R_Indicator_Child.troybin` — confiance `low`, validation manuelle obligatoire.
- `Vi_R_Jump` — `Skins/Base/Particles/Vi_R_Jump.troybin` — confiance `low`, validation manuelle obligatoire.
- `Vi_R_Jump_Arm_Wpn_Trail` — `Skins/Base/Particles/Vi_R_Jump_Arm_Wpn_Trail.troybin` — confiance `low`, validation manuelle obligatoire.
- `Vi_R_Land` — `Skins/Base/Particles/Vi_R_Land.troybin` — confiance `low`, validation manuelle obligatoire.
- `Vi_R_Run` — `Skins/Base/Particles/Vi_R_Run.troybin` — confiance `low`, validation manuelle obligatoire.
- `Vi_R_Run_Sound` — `Skins/Base/Particles/Vi_R_Run_Sound.troybin` — confiance `low`, validation manuelle obligatoire.
- `Vi_R_Skin_Swap` — `Skins/Base/Particles/Vi_R_Skin_Swap.troybin` — confiance `low`, validation manuelle obligatoire.
- `Vi_R_Skin_Swap_Jump` — `Skins/Base/Particles/Vi_R_Skin_Swap_Jump.troybin` — confiance `low`, validation manuelle obligatoire.
- `Vi_R_Voice_Special` — `Skins/Base/Particles/Vi_R_Voice_Special.troybin` — confiance `low`, validation manuelle obligatoire.

Os à valider :

- `C_BUFFBONE_GLB_CHEST_LOC` — présent dans le squelette sélectionné.
- `neck` — présent dans le squelette sélectionné.
- `R_hand` — présent dans le squelette sélectionné.

## Ordre d’implémentation spécifique à Vi

### P0 — Q, Brise-coffre

1. Au début de la charge, démarrer la famille `Spell1` et les effets `vi_q_channel_01`, `vi_q_channel_02` et `vi_q_channel_l` selon leur rôle observé.
2. Employer `Vi_Spell1_Idle` lorsque Vi charge sans se déplacer, et `Vi_Spell1_Run` lorsqu’elle se déplace. Ne pas redémarrer le clip à chaque tick.
3. La fenêtre prouvée est de `1,25 s`; l’événement calculé depuis `CastFrame` est à `0,25 s` dans le clip principal.
4. À la libération, tester `Vi_Spell3` comme animation candidate (`medium`) et confirmer par capture vidéo image par image avant de la rendre définitive.
5. Attacher les effets persistants au propriétaire approprié. `MissileBoneName=root` est prouvé pour le sort principal.
6. Sur interruption/expiration, arrêter les boucles de charge et jouer/nettoyer `vi_q_expire`. À l’impact, distinguer champion (`vi_q_tar`) et sbire (`vi_q_minion_tar`).

### P0 — E, Force excessive

1. Utiliser `Vi_Spell2` et `Vi_Spell2_A` comme variantes prouvées, en conservant une alternance déterministe si le code existant la prévoit.
2. À l’activation, relier `vi_e_activate_hands_r` et `vi_e_activate_hands_l` aux mains correspondantes et les supprimer à la consommation/expiration de la charge.
3. Les références `Malphite_Enrage_glow`, `AnnieBasicAttack_mis` et les sons Annie présentes dans l’INIBIN ressemblent à des valeurs de gabarit : ne pas les intégrer sans preuve en jeu.
4. Examiner les candidates `Vi_E_Cas`, `Vi_E_tar`, `Vi_E_Minion_tar` et `Vi_E_Shockwave_tar` dans le client et attribuer séparément cast, cône/onde et impact.

### P0 — R, Mise à l’épreuve

1. Utiliser `Vi_Spell4` pour l’entrée, `Vi_Spell4_run` pendant la poursuite et `Vi_Spell4_hit` à l’impact.
2. Le début de cast prouvé vaut `0,25 s` via `OverrideCastTime`.
3. Afficher les indicateurs de cible `vi_r_target_indicator`/`02`, puis nettoyer les deux sur annulation, mort ou impact.
4. Pendant la poursuite, relier `vi_r_dash_tar`; à l’impact, séparer `vi_r_chargedrun_impact`, `vi_r_knockback_tar`, `vi_r_pillar` et les effets de cible.
5. `Spell2` provenant de `ViRDunk` reste une preuve secondaire : vérifier si le clip s’applique à Vi, à la cible ou à un helper avant usage.
6. Ne pas utiliser les références génériques `Disintegrate`, `HeadButt`, `AnnieBasicAttack` ou `Stun_glb` sans validation explicite.

### P1 — W et passif

1. W est passif : aucune animation de cast n’est prouvée et il ne faut pas en créer une.
2. Implémenter visuellement les stacks avec `vi_armorshred_hold`, les impacts successifs `vi_armorshred_hit_1/2`, puis le proc `vi_armorshred`.
3. Différencier champion, sbire et monstre/dragon avec leurs variantes prévues.
4. Pour le bouclier passif, utiliser les effets `vi_passive_ready`, `vi_passive_shield`, mains gauche/droite et désactivation, avec nettoyage garanti.

## Tests d’acceptation obligatoires

- Aucun effet ne reste au sol ou sur un ancien propriétaire après déplacement, mort, interruption ou fin de buff.
- Les effets attachés suivent l’os à chaque frame et ne sont pas recréés à chaque tick.
- Un changement de visibilité ne rejoue ni cast, ni spawn, ni animation initiale.
- Deux clients voient le même clip, la même phase et la même suppression d’effet.
- Une interruption de Q est testée au début, au milieu et juste avant la fin de charge.
- Q est testé immobile, en déplacement, contre champion, contre sbire et sans toucher de cible.
- E est testé sur les deux variantes de poing, avec plusieurs charges et expiration.
- R est testé sur toute la poursuite, sur mort/disparition de cible et à l’impact.
- W est testé aux premier, deuxième et troisième stacks, puis après expiration et réapplication.
- Le nombre d’effets vivants revient à sa valeur initiale après chaque scénario.

## Format du compte rendu demandé à l’IA

Pour chaque changement, fournir : fichier et méthode modifiés, preuve issue de ce contrat, événement réseau/client utilisé, propriétaire et os de l’effet, règle de suppression, test ajouté, résultat en jeu et incertitudes restantes. Ne jamais annoncer « parfait » sans comparaison vidéo ou capture paquet correspondante.

## Sources locales faisant autorité

- Contrat machine : `visual-contract.json` généré pour `Vi`.
- Rapport humain : `visual-contract.md`.
- Racine analysée : `/Users/mathieuv/Documents/Amazon/vi-visual-source/Vi`.
