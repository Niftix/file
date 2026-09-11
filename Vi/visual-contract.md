# Vi (Base) — contrat visuel LoL 4.20

Généré avec `lol420-visual-contract 0.1.0`.

## Inventaire

- `file_count` : 463
- `inibin_count` : 34
- `luaobj_count` : 54
- `preload_count` : 26
- `animation_count` : 37
- `skeleton_count` : 1
- `particle_count` : 96
- `unresolved_dependency_count` : 7

## Q

Entrées : `viq`

### Séquence proposée

- **cast** — INIBIN animation/timing (high)
- **channel_or_loop** — preload/ANM naming (medium)
- **movement_or_missile** — dependent spell graph (medium)
- **impact** — INIBIN/dependent spell (high)
- **winddown** — INIBIN animation (high)

### Animations

- `Vi_Spell1` — 1.6667s, 30.0 fps — high — `Skins/Base/Animations/Vi_Spell1.anm`
- `Vi_Spell1_Idle` — 0.9032s, 31.0 fps — high — `Skins/Base/Animations/Vi_Spell1_Idle.anm`
- `Vi_SPELL1_IdleIntro` — 2.0s, 30.0 fps — high — `Skins/Base/Animations/Vi_SPELL1_IdleIntro.anm`
- `Vi_Spell1_Run` — 1.2333s, 30.0 fps — high — `Skins/Base/Animations/Vi_Spell1_Run.anm`
- `Vi_Spell3` — 1.7s, 30.0 fps — medium — `Skins/Base/Animations/Vi_Spell3.anm`

### Temporalité calculée

- `cast_event_seconds` : `0.25`
- `cast_event_basis` : `SpellData.CastFrame / Vi_Spell1 fps`
- `confidence` : `high`
- `channel_duration_seconds` : `1.25`

### Champs et timings prouvés

- `Sound_CastName` = `none.wav` — high — `Spells/ViQ.inibin`
- `MissileBoneName` = `root` — high — `Spells/ViQ.inibin`
- `Sound_HitName` = `none.wav` — high — `Spells/ViQ.inibin`
- `AnimationWinddownName` = `Spell1_Fire` — high — `Spells/ViQ.inibin`
- `ChannelDuration` = `1.25` — high — `Spells/ViQ.inibin`
- `CastFrame` = `7.5` — high — `Spells/ViQ.inibin`
- `DelayCastOffsetPercent` = `65535` — high — `Spells/ViQ.inibin`
- `DelayTotalTimePercent` = `65535` — high — `Spells/ViQ.inibin`
- `UseAnimatorFramerate` = `True` — high — `Spells/ViQ.inibin`
- `MissileSpeed` = `1500.0000` — high — `Spells/ViQ.inibin`
- `AnimationName` = `Spell3` — medium — `Spells/ViQLaunch.inibin`
- `DelayCastOffsetPercent` = `-0.5` — medium — `Spells/ViQLaunch.inibin`
- `DelayTotalTimePercent` = `-0.5` — medium — `Spells/ViQLaunch.inibin`
- `CastFrame` = `1.9800000190734863` — medium — `Spells/ViQLaunch.inibin`
- `MissileSpeed` = `1200.0000` — medium — `Spells/ViQLaunch.inibin`

### Particules

- `vi_armorshred.troy` → `Skins/Base/Particles/Vi_ArmorShred.troybin` — `selected_skin`
- `vi_armorshred_dragon.troy` → `Skins/Base/Particles/VI_ArmorShred_Dragon.troybin` — `selected_skin`
- `vi_armorshred_hit_1.troy` → `Skins/Base/Particles/Vi_ArmorShred_Hit_1.troybin` — `selected_skin`
- `vi_armorshred_hit_2.troy` → `Skins/Base/Particles/Vi_ArmorShred_Hit_2.troybin` — `selected_skin`
- `vi_armorshred_hit_minion_1.troy` → `Skins/Base/Particles/Vi_ArmorShred_Hit_Minion_1.troybin` — `selected_skin`
- `vi_armorshred_hit_minion_2.troy` → `Skins/Base/Particles/Vi_ArmorShred_Hit_Minion_2.troybin` — `selected_skin`
- `vi_armorshred_hold.troy` → `Skins/Base/Particles/Vi_ArmorShred_hold.troybin` — `selected_skin`
- `vi_armorshred_minion.troy` → `Skins/Base/Particles/Vi_ArmorShred_Minion.troybin` — `selected_skin`
- `vi_attack_speed_buff.troy` → `Skins/Base/Particles/Vi_Attack_Speed_Buff.troybin` — `selected_skin`
- `vi_e_attackspeed_knuckles.troy` → `Skins/Base/Particles/VI_E_AttackSpeed_Knuckles.troybin` — `selected_skin`
- `vi_passive_buff.troy` → `Skins/Base/Particles/Vi_Passive_Buff.troybin` — `selected_skin`
- `vi_passive_buff_deactivate.troy` → `Skins/Base/Particles/Vi_Passive_Buff_DeActivate.troybin` — `selected_skin`
- `vi_passive_hand_l.troy` → `Skins/Base/Particles/Vi_passive_Hand_L.troybin` — `selected_skin`
- `vi_passive_hand_r.troy` → `Skins/Base/Particles/Vi_passive_Hand_R.troybin` — `selected_skin`
- `vi_passive_shield.troy` → `Skins/Base/Particles/Vi_Passive_Shield.troybin` — `selected_skin`
- `vi_q_channel_01.troy` → `Skins/Base/Particles/Vi_Q_Channel_01.troybin` — `selected_skin`
- `vi_q_channel_02.troy` → `Skins/Base/Particles/Vi_Q_Channel_02.troybin` — `selected_skin`
- `vi_q_channel_l.troy` → `Skins/Base/Particles/Vi_Q_Channel_L.troybin` — `selected_skin`
- `vi_q_expire.troy` → `Skins/Base/Particles/Vi_Q_Expire.troybin` — `selected_skin`
- `vi_q_minion_tar.troy` → `Skins/Base/Particles/Vi_Q_Minion_tar.troybin` — `selected_skin`
- `vi_q_tar.troy` → `Skins/Base/Particles/Vi_Q_tar.troybin` — `selected_skin`

### Os d’attache

- `root` — présent

## W

Entrées : `viw`

### Séquence proposée

- Aucune phase suffisamment étayée.

### Animations

- Aucune animation associée.

### Temporalité calculée

- Aucune temporalité ne peut être calculée sans hypothèse supplémentaire.

### Champs et timings prouvés

- `HitBoneName` = `C_BUFFBONE_GLB_HEAD_LOC` — high — `Spells/ViW.inibin`
- `MissileBoneName` = `R_hand` — high — `Spells/ViW.inibin`
- `DelayCastOffsetPercent` = `-0.5` — high — `Spells/ViW.inibin`
- `DelayTotalTimePercent` = `-0.5` — high — `Spells/ViW.inibin`
- `CastFrame` = `1.9800000190734863` — high — `Spells/ViW.inibin`
- `MissileSpeed` = `1200.0000` — high — `Spells/ViW.inibin`

### Particules

- `vi_armorshred.troy` → `Skins/Base/Particles/Vi_ArmorShred.troybin` — `selected_skin`
- `vi_armorshred_dragon.troy` → `Skins/Base/Particles/VI_ArmorShred_Dragon.troybin` — `selected_skin`
- `vi_armorshred_hold.troy` → `Skins/Base/Particles/Vi_ArmorShred_hold.troybin` — `selected_skin`
- `vi_armorshred_minion.troy` → `Skins/Base/Particles/Vi_ArmorShred_Minion.troybin` — `selected_skin`
- `vi_attack_speed_buff.troy` → `Skins/Base/Particles/Vi_Attack_Speed_Buff.troybin` — `selected_skin`
- `vi_e_attackspeed_knuckles.troy` → `Skins/Base/Particles/VI_E_AttackSpeed_Knuckles.troybin` — `selected_skin`
- `vi_passive_buff.troy` → `Skins/Base/Particles/Vi_Passive_Buff.troybin` — `selected_skin`
- `vi_passive_buff_deactivate.troy` → `Skins/Base/Particles/Vi_Passive_Buff_DeActivate.troybin` — `selected_skin`
- `vi_passive_hand_l.troy` → `Skins/Base/Particles/Vi_passive_Hand_L.troybin` — `selected_skin`
- `vi_passive_hand_r.troy` → `Skins/Base/Particles/Vi_passive_Hand_R.troybin` — `selected_skin`
- `vi_passive_shield.troy` → `Skins/Base/Particles/Vi_Passive_Shield.troybin` — `selected_skin`

### Os d’attache

- `C_BUFFBONE_GLB_HEAD_LOC` — présent
- `R_hand` — présent

## E

Entrées : `vie`

### Séquence proposée

- **cast** — INIBIN animation/timing (high)
- **impact** — INIBIN/dependent spell (high)

### Animations

- `Vi_Spell2` — 1.7s, 30.0 fps — high — `Skins/Base/Animations/Vi_Spell2.anm`
- `Vi_Spell2_A` — 1.7s, 30.0 fps — high — `Skins/Base/Animations/Vi_Spell2_A.anm`

### Temporalité calculée

- Aucune temporalité ne peut être calculée sans hypothèse supplémentaire.

### Champs et timings prouvés

- `HitEffectName` = `Malphite_Enrage_glow.troy` — high — `Spells/ViE.inibin`
- `HitBoneName` = `root` — high — `Spells/ViE.inibin`
- `AfterEffectName` = `Malphite_Enrage_glow.troy` — high — `Spells/ViE.inibin`
- `AnimationName` = `Spell2` — high — `Spells/ViE.inibin`
- `Sound_CastName` = `Annie_Incinerate_3.wav` — high — `Spells/ViE.inibin`
- `MissileBoneName` = `R_hand` — high — `Spells/ViE.inibin`
- `MissileEffect` = `AnnieBasicAttack_mis.troy` — high — `Spells/ViE.inibin`
- `Sound_HitName` = `none.wav` — high — `Spells/ViE.inibin`
- `DelayCastOffsetPercent` = `-0.5` — high — `Spells/ViE.inibin`
- `DelayTotalTimePercent` = `-0.5` — high — `Spells/ViE.inibin`
- `CastFrame` = `.5` — high — `Spells/ViE.inibin`

### Particules

- `anniebasicattack_mis.troy` → `non résolue/localisée hors du champion` — `unresolved`
- `malphite_enrage_glow.troy` → `non résolue/localisée hors du champion` — `unresolved`
- `vi_e_activate_hands_l.troy` → `Skins/Base/Particles/Vi_E_activate_hands_L.troybin` — `selected_skin`
- `vi_e_activate_hands_r.troy` → `Skins/Base/Particles/Vi_E_activate_hands_R.troybin` — `selected_skin`
- `vi_passive_buff.troy` → `Skins/Base/Particles/Vi_Passive_Buff.troybin` — `selected_skin`
- `vi_passive_buff_deactivate.troy` → `Skins/Base/Particles/Vi_Passive_Buff_DeActivate.troybin` — `selected_skin`
- `vi_passive_hand_l.troy` → `Skins/Base/Particles/Vi_passive_Hand_L.troybin` — `selected_skin`
- `vi_passive_hand_r.troy` → `Skins/Base/Particles/Vi_passive_Hand_R.troybin` — `selected_skin`
- `vi_passive_shield.troy` → `Skins/Base/Particles/Vi_Passive_Shield.troybin` — `selected_skin`

### Os d’attache

- `R_hand` — présent
- `root` — présent

## R

Entrées : `vir`

### Séquence proposée

- **cast** — INIBIN animation/timing (high)
- **impact** — INIBIN/dependent spell (high)

### Animations

- `Vi_Spell2` — 1.7s, 30.0 fps — medium — `Skins/Base/Animations/Vi_Spell2.anm`
- `Vi_Spell2_A` — 1.7s, 30.0 fps — medium — `Skins/Base/Animations/Vi_Spell2_A.anm`
- `Vi_Spell4` — 0.6452s, 31.0 fps — high — `Skins/Base/Animations/Vi_Spell4.anm`
- `Vi_Spell4_hit` — 0.9355s, 31.0 fps — high — `Skins/Base/Animations/Vi_Spell4_hit.anm`
- `Vi_Spell4_run` — 1.0s, 31.0 fps — high — `Skins/Base/Animations/Vi_Spell4_run.anm`

### Temporalité calculée

- `cast_event_seconds` : `0.25`
- `cast_event_basis` : `SpellData.OverrideCastTime`
- `confidence` : `high`

### Champs et timings prouvés

- `HitEffectName` = `DisintegrateHit_tar.troy` — high — `Spells/ViR.inibin`
- `AfterEffectName` = `Disintegrate_tar.troy` — high — `Spells/ViR.inibin`
- `AnimationName` = `Spell4` — high — `Spells/ViR.inibin`
- `Sound_CastName` = `ability_disintegrate_cast.wav` — high — `Spells/ViR.inibin`
- `MissileBoneName` = `neck` — high — `Spells/ViR.inibin`
- `MissileEffect` = `Disintegrate_mis.troy` — high — `Spells/ViR.inibin`
- `Sound_HitName` = `ability_disintegrate_hit.wav` — high — `Spells/ViR.inibin`
- `OverrideCastTime` = `0.25` — high — `Spells/ViR.inibin`
- `DelayCastOffsetPercent` = `-0.5` — high — `Spells/ViR.inibin`
- `DelayTotalTimePercent` = `-0.5` — high — `Spells/ViR.inibin`
- `CastFrame` = `7.5` — high — `Spells/ViR.inibin`
- `UseAnimatorFramerate` = `True` — high — `Spells/ViR.inibin`
- `MissileSpeed` = `1400.0000` — high — `Spells/ViR.inibin`
- `HitEffectName` = `HeadButt_tar.troy` — medium — `Spells/ViRDunk.inibin`
- `HitBoneName` = `C_BUFFBONE_GLB_CHEST_LOC` — medium — `Spells/ViRDunk.inibin`
- `AfterEffectName` = `Stun_glb.troy` — medium — `Spells/ViRDunk.inibin`
- `AnimationName` = `Spell2` — medium — `Spells/ViRDunk.inibin`
- `Sound_CastName` = `Minotaur_Headbutt.wav` — medium — `Spells/ViRDunk.inibin`
- `MissileBoneName` = `R_hand` — medium — `Spells/ViRDunk.inibin`
- `MissileEffect` = `AnnieBasicAttack_mis.troy` — medium — `Spells/ViRDunk.inibin`
- `Sound_HitName` = `none.wav` — medium — `Spells/ViRDunk.inibin`
- `DelayTotalTimePercent` = `-0.550000011920929` — medium — `Spells/ViRDunk.inibin`
- `DelayCastOffsetPercent` = `0.8` — medium — `Spells/ViRDunk.inibin`
- `CastFrame` = `33` — medium — `Spells/ViRDunk.inibin`
- `UseAnimatorFramerate` = `True` — medium — `Spells/ViRDunk.inibin`

### Particules

- `anniebasicattack_mis.troy` → `non résolue/localisée hors du champion` — `unresolved`
- `disintegrate_mis.troy` → `non résolue/localisée hors du champion` — `unresolved`
- `disintegrate_tar.troy` → `non résolue/localisée hors du champion` — `unresolved`
- `disintegratehit_tar.troy` → `non résolue/localisée hors du champion` — `unresolved`
- `headbutt_tar.troy` → `non résolue/localisée hors du champion` — `unresolved`
- `stun_glb.troy` → `non résolue/localisée hors du champion` — `unresolved`
- `vi_r_chargedrun_impact.troy` → `Skins/Base/Particles/Vi_R_ChargedRun_impact.troybin` — `selected_skin`
- `vi_r_dash_tar.troy` → `Skins/Base/Particles/Vi_R_Dash_tar.troybin` — `selected_skin`
- `vi_r_knockback_tar.troy` → `Skins/Base/Particles/Vi_R_Knockback_tar.troybin` — `selected_skin`
- `vi_r_laser_target.troy` → `Skins/Base/Particles/Vi_R_Laser_Target.troybin` — `selected_skin`
- `vi_r_pillar.troy` → `Skins/Base/Particles/Vi_R_Pillar.troybin` — `selected_skin`
- `vi_r_target_indicator.troy` → `Skins/Base/Particles/Vi_R_target_Indicator.troybin` — `selected_skin`
- `vi_r_target_indicator_02.troy` → `Skins/Base/Particles/Vi_R_target_Indicator_02.troybin` — `selected_skin`
- `vi_racer_r_pillar.troy` → `Skins/Skin01/Particles/Vi_Racer_R_Pillar.troybin` — `other_skin`

### Os d’attache

- `C_BUFFBONE_GLB_CHEST_LOC` — présent
- `neck` — présent
- `R_hand` — présent

## Limites

Le rapport sépare les faits lus dans les ressources des inférences par convention de nommage. Une chronologie exacte issue du bytecode nécessiterait un décompilateur Lua 5.1 et une analyse sémantique supplémentaires.
