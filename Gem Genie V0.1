from pynput import keyboard
from PIL import ImageGrab
import pydirectinput
import numpy as np
import threading
import time
import cv2
import sys
import os
import functools
import ctypes
import pygetwindow as gw
import win32gui, win32con, win32api
from pywinauto import Application
import pyautogui

# DESCRIPTION: Gem Genie Macro
# VERSIONS: all

version = "v35.1"
try:
    from ahk import AHK
    base_path = getattr(sys, '_MEIPASS', os.path.dirname(os.path.abspath(__file__)))
    bundled_ahk = os.path.join(base_path, 'AutoHotkey.exe')
    installed_ahk = r"C:\Program Files\AutoHotkey\AutoHotkey.exe"

    ahk_exe_path = bundled_ahk if os.path.exists(bundled_ahk) else installed_ahk
    ahk = AHK(executable_path=ahk_exe_path)
except Exception as e:
    ctypes.windll.user32.MessageBoxW(
        0,
        f"AutoHotkey could not be loaded from either bundled or installed path.\n\nError: {e}",
        "AutoHotkey Error",
        0x10
    )
    sys.exit()

SCRIPT_DIR = os.path.dirname(os.path.abspath(__file__))
IMG_SCR = os.path.join(os.path.expanduser("~"), "MacroClient", "Images")

CRYSTALS_BASE = "crystals.png"
QUEST_FILE_NAMES = [
    "common.png", # 1
    "spotted.png", # 2
    "iceshard.png", # 3
    "spikey.png", # 4
    "magma.png", # 5
    "crystal.png", # 6
    "lunar.png", # 7
    "void.png", # 8
    "hell.png", # 9
    "nightmare.png", # 10
    "rainbow.png", # 11
    "showman.png", # 12
    "mining.png", # 13
    "cyber.png", # 14
    "neon.png", # 15
    "icy.png", # 16
    "vine.png", # 17
    "lava.png", # 18
    "atlantis.png", # 19
    "classic.png", # 20
    "Rcommon.png", # 21
    "Rrare.png", # 22
    "Runique.png", # 23
    "Repic.png", # 24
    "Rlegendary.png", # 25
    "bubble1m.png", # 26
    "bubble6m.png", # 27
    "coins2m.png", # 28
    "coins10m.png", # 29
    "egg3k.png", # 30
    "egg7k.png", # 31
    "gingerbread.png", # 32
    "candycane.png", # 33
    "yuletide.png", # 34
    "northpole.png", # 35
    "aurora.png", # 36
    "festive.png", # 37
]
img_suffix = None
egg_choices = {0: "infinity"}


def img_variant(filename, suffix):
    base, ext = os.path.splitext(filename)
    return f"{base}{suffix}{ext}"


def img_exists(filename):
    search_roots = [SCRIPT_DIR, base_path, IMG_SCR]
    for root in search_roots:
        if not root:
            continue
        candidate = os.path.join(root, filename)
        if os.path.exists(candidate):
            return True
    return False


def get_suffix():
    global img_suffix
    if img_suffix is not None:
        return img_suffix
    for suffix in ("", "2", "3"):
        candidate = img_variant(CRYSTALS_BASE, suffix)
        if img_exists(candidate):
            img_suffix = suffix
            break
    if img_suffix is None:
        img_suffix = ""
    if img_suffix:
        print(f"[ASSETS] Using quest image suffix '{img_suffix}'")
    return img_suffix


def asset_display_name(filename, suffix=None):
    base = os.path.splitext(os.path.basename(filename))[0]
    suffix = img_suffix if suffix is None else suffix
    if suffix and base.endswith(suffix):
        return base[:-len(suffix)]
    return base


img_suffix = get_suffix()
CRYSTALS = img_variant(CRYSTALS_BASE, img_suffix)
QUESTS = [img_variant(name, img_suffix) for name in QUEST_FILE_NAMES]

event_egg_list = 21
event_egg_id = 100
blow_bubbles_option = event_egg_list + 1
BLOW_BUBBLES_ACTION = "blow_bubbles"
waiting_eggs = QUESTS[:20]

egg_choices = {0: "infinity"}
for idx, file_name in enumerate(waiting_eggs, start=1):
    egg_choices[idx] = asset_display_name(file_name)
egg_choices[event_egg_list] = "2026 Event"
egg_choices[blow_bubbles_option] = "blow bubbles"

wait_egg_target = {0: None}
for idx in range(1, len(waiting_eggs) + 1):
    wait_egg_target[idx] = idx
wait_egg_target[event_egg_list] = event_egg_id
wait_egg_target[blow_bubbles_option] = BLOW_BUBBLES_ACTION

WINTER_QUEST_IDS = {32, 33, 34, 35, 36, 37}

# global names
TIME_switch = keyboard.Key.f1
ON_switch = keyboard.Key.f2
OFF_switch = keyboard.Key.f3

# variables
running_flag = False    
total_time = ""
wait = 3
card_choice = {
    1: (169, 536),
    2: (409, 535),
    3: (654, 537),
}
reroll = (408, 604)
down = (665, 520)
up = (665, 170)
teleport = (403, 617)
crystals_template = None
quest_templates = []
box_template = None
REWARD_MATCH = 0.9
QUEST_MATCH = 0.75
one_scroll = True
bubble_count = 100000
center = (382, 322)
items = (15, 346)
box_region = (202, 175, 751, 565)
use = (121, 488)
use50 = (558, 413)
egg_count = 12
wait_egg = 0
daily = (47, 327)
daily_col = (239, 60, 104)
hatch_overrides = {21: 350, 22: 300, 23: 500, 30: 3000, 31: 7500}
gui = (726, 109)
gui_col = (197, 19, 76)
bp_max = (432, 354)
bp_max_col = (125, 243, 19)
auto_hatch = False
box = (95, 240)
box_col = (0, 0, 244)
box_flag = False
reroll_count = 0
moved = False
no_orbs = (449, 410)
no_orbs_col = (221, 40, 74)
last_time = None

CARD_REWARD_RECTS_RAW = {
    1: ((55, 430), (282, 487)),
    2: ((293, 430), (522, 487)),
    3: ((528, 430), (765, 487)),
}

card_quests = {
    1: [
        ((117, 236), (248, 266)),
        ((117, 268), (248, 307)),
        ((117, 309), (248, 347)),
    ],
    2: [
        ((358, 236), (485, 266)),
        ((358, 268), (485, 307)),
        ((358, 309), (485, 347)),
    ],
    3: [
        ((597, 236), (730, 266)),
        ((597, 268), (730, 307)),
        ((597, 309), (730, 347)),
    ],
}

CARD_REWARD_RECTS = {
    1: ((67, 427), (264, 481)),
    2: ((314, 423), (504, 488)),
    3: ((551, 426), (745, 486)),
}
CARD_QUEST_RECTS = card_quests


print = functools.partial(print, flush=True)

def setup_roblox_window():
    rblx = [w for w in gw.getWindowsWithTitle('Roblox') if w.title == 'Roblox']
    if len(rblx) != 1:
        print("More than 1 roblox game running or no Roblox window found close all other instances" if len(rblx) > 1 else "No Roblox window found")
        return False
    
    try:
        window = rblx[0]
        hwnd = window._hWnd
        win32gui.SetForegroundWindow(hwnd)

        style = win32gui.GetWindowLong(hwnd, win32con.GWL_STYLE)
        if not (style & win32con.WS_CAPTION):
            Application().connect(handle=hwnd).window(handle=hwnd).type_keys('{F11}')
            time.sleep(1)

        new_style = win32con.WS_OVERLAPPEDWINDOW
        win32gui.SetWindowLong(hwnd, win32con.GWL_STYLE, new_style)

        rect = win32gui.GetClientRect(hwnd)
        window_rect = win32gui.GetWindowRect(hwnd)
        border_height = (window_rect[3] - window_rect[1]) - (rect[3] - rect[1])
        
        total_width = 800
        total_height = 630 + border_height

        win32gui.SetWindowPos(
            hwnd,
            win32con.HWND_TOP,
            0, 0,
            total_width, total_height,
            win32con.SWP_SHOWWINDOW
        )
        return True
        
    except Exception as e:
        print(f"Error setting up Roblox window: {e}")
        return False

def load_template(filename):
    path = img_path(filename)
    if not os.path.exists(path):
        return None
    template = cv2.imread(path, cv2.IMREAD_COLOR)
    return template


def frame(bbox=None):
    screenshot = ImageGrab.grab(bbox=bbox)
    try:
        return cv2.cvtColor(np.array(screenshot), cv2.COLOR_RGB2BGR)
    finally:
        screenshot.close()


def img_path(filename):
    if os.path.isabs(filename):
        return filename
    for base in (SCRIPT_DIR, base_path, IMG_SCR):
        candidate = os.path.join(base, filename)
        if os.path.exists(candidate):
            return candidate
    return os.path.join(SCRIPT_DIR, filename)


def load_assets():
    global crystals_template, quest_templates, box_template
    crystals_template = load_template(CRYSTALS)
    quest_templates = []
    if not QUESTS:
        return
    
    for idx, file_name in enumerate(QUESTS, start=1):
        template = load_template(file_name)
        if template is None:
            continue

        quest_templates.append(
            {
                "index": idx,
                "image": template,
                "name": os.path.splitext(os.path.basename(file_name))[0],
            }
        )
    box_template = load_template("box800.png")
def bubble_sanit(value):
    if not value:
        return None
    
    cleaned = value.strip().lower().replace(",", "")
    multi = 1

    if cleaned.endswith("k"):
        multi = 1000
        cleaned = cleaned[:-1]

    elif cleaned.endswith("m"):
        multi = 1000000
        cleaned = cleaned[:-1]
    try:
        base = float(cleaned)
        return int(base * multi)
    except ValueError:
        return None

def bubble_prompt():
    global bubble_count
    print("How many bubbles do you blow per click?\nUse 'k' for thousands or 'm' for millions (e.g. 2.5m)")
    while True:
        inp = input("Bubbles per click: ").strip()
        if not inp:
            break

        parsed = bubble_sanit(inp)
        if parsed and parsed > 0:
            bubble_count = parsed
            break
        print("Invalid bubble count. Please enter a positive number (accepts k/m)")

def egg_prompt():
    global egg_count
    print("How many eggs do you open at once? (1-12)")
    while True:
        inp = input("Eggs per open: ").strip()
        if not inp:
            break
        if inp.isdigit():
            eggs = int(inp)
            if 1 <= eggs <= 12:
                egg_count = eggs
                break
        print("Invalid egg count. Please enter a number from 1 to 12")


def wait_prompt():
    global wait_egg
    print("What to do while waiting for the quest? (enter the number)")

    preview = [f"{idx}: {name}" for idx, name in sorted(egg_choices.items())]
    if preview:
        print("Options:")
        for line in preview:
            print(f"  {line}")

    while True:
        choice = input("Choice number: ").strip().lower()
        if not choice:
            print(f"[INFO] Keeping option {wait_egg} ({egg_choices.get(wait_egg, 'unknown')})")
            return

        if choice.isdigit():
            value = int(choice)
            if value in egg_choices:
                wait_egg = value
                print(f"[INFO] Will do '{egg_choices[value]}' while waiting")
                return

        print("[WARN] Invalid egg number")

def delay_prompt():
    global wait
    print("How long is your gem genie quest cooldown? e.g. '15m', '500s'")
    while True:
        raw = input("Quest delay: ").strip().lower()
        if not raw:
            return

        multi = None
        if raw.endswith('m'):
            multi = 60
            raw = raw[:-1]
        elif raw.endswith('s'):
            multi = 1
            raw = raw[:-1]

        try:
            value = float(raw)
        except ValueError:
            print("Please enter a valid number (optionally suffixed with 'm' or 's')")
            continue

        if multi is None:
            multi = 1 if value > 60 else 60

        seconds = int(value * multi)
        if seconds <= 0:
            print("Delay must be positive")
            continue

        if seconds > 3600:
            print("Quest delay capped at 3600 seconds (1 hour)")
            seconds = 3600

        wait = seconds
        print(f"Quest delay set to {wait} seconds (~{wait/60:.2f} minutes)")
        time.sleep(1)
        return

def quests(image, rect):
    if image is None:
        return None
    
    (x1, y1), (x2, y2) = rect
    x1, x2 = sorted((int(x1), int(x2)))
    y1, y2 = sorted((int(y1), int(y2)))
    height, width = image.shape[:2]
    x1 = max(0, min(width, x1))
    x2 = max(0, min(width, x2))
    y1 = max(0, min(height, y1))
    y2 = max(0, min(height, y2))
    if x2 - x1 <= 0 or y2 - y1 <= 0:
        return None
    return image[y1:y2, x1:x2].copy()

def template_match(region, template):
    if region is None or template is None:
        return 0.0
    
    template_height, template_width = template.shape[:2]
    if region.shape[0] < template_height or region.shape[1] < template_width:
        return 0.0
    
    result = cv2.matchTemplate(region, template, cv2.TM_CCOEFF_NORMED)
    _, max_val, _, _ = cv2.minMaxLoc(result)
    return float(max_val)

def reward(screen):
    if crystals_template is None:
        return None, 0.0
    
    card_scores = []
    for card_index, rect in CARD_REWARD_RECTS.items():
        region = quests(screen, rect)
        score = template_match(region, crystals_template)
        card_scores.append((card_index, score))

        if score >= REWARD_MATCH:
            return card_index, score
    return None, 0.0

def list_quests(card_index, screen):
    quest_hits = []
    rects = card_quests.get(card_index, [])

    if not quest_templates:
        return [None for _ in rects]
    
    for idx, rect in enumerate(rects, start=1):
        region = quests(screen, rect)
        best_index = None
        best_score = 0.0

        for template in quest_templates:
            score = template_match(region, template["image"])
            if score > best_score:
                best_score = score
                best_index = template["index"]

        quest_hits.append(best_index if best_score >= QUEST_MATCH else None)
    return quest_hits


def board_quests(screen):
    for card_idx in card_quests.keys():
        quests_found = list_quests(card_idx, screen)
        if any(q is not None for q in quests_found):
            return True
    return False


def quest_select():
    global last_time
    last_time = time.time()


def time_left():
    if last_time is None:
        return float(wait)
    elapsed = max(0.0, time.time() - last_time)
    return max(0.0, float(wait) - elapsed)


def wait_hatch(skip_message=None):
    global auto_hatch
    remaining = time_left()
    if remaining <= 0:
        if skip_message:
            print(skip_message)
        return False

    auto_hatch = True
    try:
        while True:
            remaining = time_left()
            if remaining <= 0:
                break
            if not running_flag:
                pause()
                continue
            time.sleep(min(0.5, remaining))
    finally:
        auto_hatch = False

    time.sleep(5)
    return True


def blow_bubbles():
    global moved
    pydirectinput.keyDown('m')
    pydirectinput.keyUp('m')
    time.sleep(1.25)
    move(*down)
    for _ in range(7):
        pydirectinput.click()
        time.sleep(0.1)
    move(*teleport)
    time.sleep(2)
    move(*center)
    moved = True

    while running_flag:
        remaining = time_left()
        if remaining <= 0:
            break
        pydirectinput.click()
        time.sleep(0.1)


def cleared_quests():
    global moved
    if not running_flag:
        return False

    get_quest()
    if not running_flag:
        return False

    screen = frame()
    card_index, _ = reward(screen)

    pending_cards = []
    processed = set()

    if card_index is not None:
        quests_found = list_quests(card_index, screen)
        if any(q is not None for q in quests_found):
            pending_cards.append((card_index, quests_found))
            processed.add(card_index)

    for idx in card_quests.keys():
        if idx in processed:
            continue
        quests_found = list_quests(idx, screen)
        if any(q is not None for q in quests_found):
            pending_cards.append((idx, quests_found))

    if not pending_cards:
        print("Quest completed successfully")
        return True

    print("Quest still available, retrying quest")
    for _, quests_found in pending_cards:
        moved = False
        do_quests(quests_found)
        if not running_flag:
            return False

    return False

def open_boxes():
    global moved, handled_box, one_scroll
    egg_number = 11
    if not running_flag:
        return
    
    moved = True
    do_quests([egg_number], hatching_only=True)
    if not running_flag:
        return

    start_hatch(11)
    if not running_flag:
        return
    
    time.sleep(4)
    pydirectinput.keyDown('f')
    pydirectinput.keyUp('f')
    time.sleep(0.2)
    move(*items)
    time.sleep(0.2)
    handled_box = False

    if detect_color(box, box_col, 12):
        move(*use)
        time.sleep(0.2)
        move(*use50)
        time.sleep(1.5)

        for _ in range(20):
            pydirectinput.click()
            time.sleep(0.05)

            if not running_flag:
                one_scroll = True
                pause()
            
        time.sleep(1.5)
        handled_box = True

    else:
        move(*center)
        for _ in range(6):
            scroll('down', 700)
            time.sleep(0.2)

        top_left_x, top_left_y = box_region[0], box_region[1]
        template_h, template_w = box_template.shape[:2]
        for attempt in range(5):
            if not running_flag:
                one_scroll = True
                pause()
            
            region = frame(bbox=box_region)
            result = cv2.matchTemplate(region, box_template, cv2.TM_CCOEFF_NORMED)
            _, max_val, _, max_loc = cv2.minMaxLoc(result)

            if max_val >= 0.85:
                click_x = top_left_x + max_loc[0] + template_w // 2
                click_y = top_left_y + max_loc[1] + template_h // 2
                move(click_x, click_y)
                time.sleep(0.2)
                move(*use)
                time.sleep(0.2)
                move(*use50)
                time.sleep(1.5)

                for _ in range(20):
                    pydirectinput.click()
                    time.sleep(0.05)

                    if not running_flag:
                        one_scroll = True
                        pause()
                time.sleep(1.5)
                handled_box = True
                break

            scroll('up', 200)
            time.sleep(0.2)

    if handled_box:
        print("Quest done")
        time.sleep(2)
    moved = False

def do_quests(quest_num, hatching_only=False):
    global one_scroll, box_flag, moved
    if quest_num is None:
        quest_targets = []
    elif isinstance(quest_num, (list, tuple)):
        quest_targets = list(quest_num)
    else:
        quest_targets = [quest_num]

    processed = 0
    for quest_id in quest_targets:
        if not hatching_only and processed >= 3:
            break
        processed += 1

        if not running_flag:
            one_scroll = True
            pause()

        if not moved or quest_id in WINTER_QUEST_IDS or quest_id == event_egg_id:
            pydirectinput.keyDown('m')
            pydirectinput.keyUp('m')
            time.sleep(1.25)
            move(*down)

            if one_scroll:
                for _ in range(7):
                    pydirectinput.click()
                    time.sleep(0.1)
                one_scroll = False

            move(*teleport)
            time.sleep(2)
            if quest_id not in WINTER_QUEST_IDS and quest_id != event_egg_id:
                pydirectinput.keyDown('d')
                time.sleep(0.119)
                pydirectinput.keyUp('d')
                pydirectinput.keyDown('w')
                time.sleep(2.594)
                pydirectinput.keyUp('w')
            moved = True

        if not running_flag:
            one_scroll = True
            pause()

        if quest_id is None:
            continue

        if quest_id in (1, 2, 21):
            pydirectinput.keyDown('a')
            time.sleep(0.893)
            pydirectinput.keyUp('a')

            if quest_id in(1, 21):
                pydirectinput.keyDown('s')
                time.sleep(0.05)
                pydirectinput.keyUp('s')

            if quest_id == 2:
                pydirectinput.keyDown('w')
                time.sleep(0.092)
                pydirectinput.keyUp('w')
                pydirectinput.keyDown('a')
                time.sleep(0.060)
                pydirectinput.keyUp('a')

        elif quest_id in (3, 4, 5, 22, 23, 24, 25):
            pydirectinput.keyDown('a')
            time.sleep(0.5739)
            pydirectinput.keyUp('a')
            pydirectinput.keyDown('w')
            time.sleep(0.866)
            pydirectinput.keyUp('w')
            pydirectinput.keyDown('a')
            time.sleep(0.336)
            pydirectinput.keyUp('a')

            if quest_id in (4, 5, 23, 24, 25):
                pydirectinput.keyDown('w')
                time.sleep(0.175)
                pydirectinput.keyUp('w')

                if quest_id in (5, 23):
                    pydirectinput.keyDown('d')
                    time.sleep(0.010)
                    pydirectinput.keyUp('d')
                    pydirectinput.keyDown('w')
                    time.sleep(0.100)
                    pydirectinput.keyUp('w')

        elif quest_id in (6, 7, 8, 9):
            pydirectinput.keyDown('a')
            time.sleep(0.306)
            pydirectinput.keyUp('a')
            pydirectinput.keyDown('w')
            time.sleep(1.572)
            pydirectinput.keyUp('w')

            if quest_id == 6:
                pydirectinput.keyDown('a')
                time.sleep(0.125)
                pydirectinput.keyUp('a')

            if quest_id in (8, 9):
                pydirectinput.keyDown('d')
                time.sleep(0.225)
                pydirectinput.keyUp('d')
                pydirectinput.keyDown('w')
                time.sleep(0.05)
                pydirectinput.keyUp('w')

                if quest_id == 9:
                    pydirectinput.keyDown('d')
                    time.sleep(0.217)
                    pydirectinput.keyUp('d')

        elif quest_id == 10:
            pydirectinput.keyDown('d')
            time.sleep(0.433)
            pydirectinput.keyUp('d')
            pydirectinput.keyDown('w')
            time.sleep(1.661)
            pydirectinput.keyUp('w')

        elif quest_id in (11, 12):
            pydirectinput.keyDown('d')
            time.sleep(0.616)
            pydirectinput.keyUp('d')
            pydirectinput.keyDown('w')
            time.sleep(1.246)
            pydirectinput.keyUp('w')
            pydirectinput.keyDown('d')
            time.sleep(0.1)
            pydirectinput.keyUp('d')

            if quest_id == 11:
                pydirectinput.keyDown('w')
                time.sleep(0.175)
                pydirectinput.keyUp('w')

        elif quest_id in (13, 14, 15):
            pydirectinput.keyDown('d')
            time.sleep(0.698)
            pydirectinput.keyUp('d')

            if quest_id == 13:
                pydirectinput.keyDown('w')
                time.sleep(0.893)
                pydirectinput.keyUp('w')
                pydirectinput.keyDown('d')
                time.sleep(0.257)
                pydirectinput.keyUp('d')

            if quest_id in (14, 15):
                pydirectinput.keyDown('d')
                time.sleep(0.142)
                pydirectinput.keyUp('d')

                if quest_id == 14:
                    pydirectinput.keyDown('w')
                    time.sleep(0.113)
                    pydirectinput.keyUp('w')

                if quest_id == 15:
                    pydirectinput.keyDown('s')
                    time.sleep(0.213)
                    pydirectinput.keyUp('s')

        elif quest_id in (16, 17, 18, 19, 20):
            pydirectinput.keyDown('a')
            time.sleep(0.578)
            pydirectinput.keyUp('a')
            pydirectinput.keyDown('w')
            time.sleep(0.5234)
            pydirectinput.keyUp('w')
            pydirectinput.keyDown('a')
            time.sleep(0.9931)
            pydirectinput.keyUp('a')
            pydirectinput.keyDown('s')
            time.sleep(0.484)
            pydirectinput.keyUp('s')

            if quest_id in (16, 17, 18, 19):
                pydirectinput.keyDown('d')
                time.sleep(0.055)
                pydirectinput.keyUp('d')
                pydirectinput.keyDown('s')
                time.sleep(0.135)
                pydirectinput.keyUp('s')

                if quest_id in (16, 17, 18):
                    pydirectinput.keyDown('d')
                    time.sleep(0.041)
                    pydirectinput.keyUp('d')
                    pydirectinput.keyDown('s')
                    time.sleep(0.212)
                    pydirectinput.keyUp('s')

                    if quest_id in (16, 17):
                        pydirectinput.keyDown('d')
                        time.sleep(0.099)
                        pydirectinput.keyUp('d')
                        pydirectinput.keyDown('s')
                        time.sleep(0.136)
                        pydirectinput.keyUp('s')

                        if quest_id == 16:
                            pydirectinput.keyDown('d')
                            time.sleep(0.150)
                            pydirectinput.keyUp('d')
                            pydirectinput.keyDown('s')
                            time.sleep(0.155)
                            pydirectinput.keyUp('s')

        elif quest_id in (26, 27, 28, 29):
            moved = True
            if quest_id in (26, 27):
                total = 0
                target_amount = 1500000 if quest_id == 26 else 6000000
                nomove(*center)

                while total < target_amount:
                    if not running_flag:
                        one_scroll = True
                        pause()
                    pydirectinput.click()
                    total += bubble_count
                    time.sleep(0.65)

                    if detect_color(bp_max, bp_max_col, 10):
                        one_scroll = True
                        move(*bp_max)
                        time.sleep(5)
                        for _ in range(3):
                            pydirectinput.click()
                            time.sleep(0.6)
                pydirectinput.click()

            if quest_id in (28, 29):
                open_boxes()
                print("Box Quest done")
                continue

        elif quest_id in (30, 31):
            selected_egg_id = wait_egg_target.get(wait_egg)
            if selected_egg_id == BLOW_BUBBLES_ACTION:
                blow_bubbles()
            elif selected_egg_id is not None:
                do_quests([selected_egg_id], hatching_only=True)
            else:
                pydirectinput.keyDown('w')
                time.sleep(0.2035)
                pydirectinput.keyUp('w')
        elif quest_id in WINTER_QUEST_IDS:
            moved = True
            pydirectinput.keyDown('d')
            time.sleep(0.207)
            pydirectinput.keyUp('d')
            pydirectinput.keyDown('s')
            time.sleep(1.066)
            pydirectinput.keyUp('s')
            pydirectinput.keyDown('a')
            time.sleep(0.549)
            pydirectinput.keyUp('a')
            time.sleep(2.5)
            pydirectinput.keyDown('s')
            time.sleep(1.949)
            pydirectinput.keyUp('s')
            pydirectinput.keyDown('a')
            time.sleep(0.287)
            pydirectinput.keyUp('a')
            pydirectinput.keyDown('s')
            time.sleep(0.860)
            pydirectinput.keyUp('s')
            pydirectinput.keyDown('d')
            time.sleep(0.130)
            pydirectinput.keyUp('d')
            pydirectinput.keyDown('s')
            time.sleep(1.674)
            pydirectinput.keyUp('s')
            pydirectinput.keyDown('a')
            time.sleep(1.836)
            pydirectinput.keyUp('a')
            pydirectinput.keyDown('w')
            time.sleep(0.350)
            pydirectinput.keyUp('w')
            pydirectinput.keyDown('a')
            time.sleep(0.492)
            pydirectinput.keyUp('a')
            pydirectinput.keyDown('w')
            time.sleep(0.433)
            pydirectinput.keyUp('w')
            pydirectinput.keyDown('a')
            time.sleep(1.437)
            pydirectinput.keyUp('a')
            pydirectinput.keyDown('w')
            time.sleep(0.205)
            pydirectinput.keyUp('w')
            if quest_id in (33, 34, 35, 36, 37):
                pydirectinput.keyDown('d')
                time.sleep(0.167)
                pydirectinput.keyUp('d')
                pydirectinput.keyDown('w')
                time.sleep(0.123)
                pydirectinput.keyUp('w')
                if quest_id in (34, 35, 36, 37):
                    pydirectinput.keyDown('d')
                    time.sleep(0.250)
                    pydirectinput.keyUp('d')
                    pydirectinput.keyDown('w')
                    time.sleep(0.132)
                    pydirectinput.keyUp('w')
                    if quest_id in (35, 36, 37):
                        pydirectinput.keyDown('d')
                        time.sleep(0.178)
                        pydirectinput.keyUp('d')
                        pydirectinput.keyDown('w')
                        time.sleep(0.068)
                        pydirectinput.keyUp('w')
                        if quest_id in (36, 37):
                            pydirectinput.keyDown('d')
                            time.sleep(0.183)
                            pydirectinput.keyUp('d')
                            pydirectinput.keyDown('w')
                            time.sleep(0.124)
                            pydirectinput.keyUp('w')
                            if quest_id == 37:
                                pydirectinput.keyDown('d')
                                time.sleep(0.183)
                                pydirectinput.keyUp('d')
                                pydirectinput.keyDown('w')
                                time.sleep(0.124)
                                pydirectinput.keyUp('w')

        elif quest_id == event_egg_id:
            moved = True
            pydirectinput.keyDown('s')
            time.sleep(2.467)
            pydirectinput.keyUp('s')
            pydirectinput.keyDown('a')
            time.sleep(0.085)
            pydirectinput.keyUp('a')

        print("Completing quest id:", quest_id)
        if hatching_only:
            moved = False
            print("At egg")
            break

        if quest_id not in (26, 27, 28, 29):
            hatch_target = hatch_overrides.get(quest_id, 190)
            start_hatch(hatch_target)
            time.sleep(5)
            moved = False
        print("Quest done")
    one_scroll = True

def start_hatch(total):
    global auto_hatch
    hatched = 0
    auto_hatch = True
    try:
        while hatched < total:
            if not running_flag:
                pause()
                continue
            if not detect_color(daily, daily_col, 10):
                hatched += egg_count
                pydirectinput.keyDown('shift')
                pydirectinput.keyDown('l')
                pydirectinput.keyUp('l')
                pydirectinput.keyUp('shift')
                time.sleep(0.05)
    finally:
        auto_hatch = False

def fast_hatch():
    while True:
        if auto_hatch and running_flag:
            pydirectinput.keyDown('e')
            pydirectinput.keyUp('e')
            time.sleep(0.1)
        else:
            time.sleep(0.3)

def get_quest():
    global reroll_count
    temp_flag = False
    while True:
        if not running_flag:
            pause()
        
        pydirectinput.keyDown('m')
        pydirectinput.keyUp('m')
        time.sleep(1.25)

        if temp_flag == False:
            nomove(*up)

            for _ in range(5):
                pydirectinput.click()
                time.sleep(0.1)
                temp_flag = True

        move(*teleport)
        time.sleep(2)
        pydirectinput.keyDown('w')
        time.sleep(0.880)
        pydirectinput.keyUp('w')
        pydirectinput.keyDown('d')
        time.sleep(1.265)
        pydirectinput.keyUp('d')
        time.sleep(0.5)

        if detect_color(gui, gui_col, 15):
            break

    move(*reroll)
    reroll_count += 1
    if reroll_count % 20 == 0:
        no_orb_check()
    time.sleep(0.3)

def no_orb_check():
    global auto_hatch, moved
    pydirectinput.keyDown('i')
    time.sleep(0.1)
    pydirectinput.keyUp('i')
    pydirectinput.keyDown('o')
    time.sleep(0.4)
    pydirectinput.keyUp('o')
    if detect_color(no_orbs, no_orbs_col, 15):
        print("No orbs left, hatching the selected egg")
        move(*no_orbs)
        at_egg = False
        target_wait_id = wait_egg_target.get(wait_egg)
        if target_wait_id is not None:
            if target_wait_id == BLOW_BUBBLES_ACTION:
                blow_bubbles()
            else:
                do_quests([target_wait_id], hatching_only=True)
            at_egg = True

        if not at_egg:
            if not moved:
                pydirectinput.keyDown('m')
                pydirectinput.keyUp('m')
                time.sleep(1.25)
                move(*down)

                for _ in range(7):
                    pydirectinput.click()
                    time.sleep(0.1)

                move(*teleport)
                time.sleep(2)
                pydirectinput.keyDown('d')
                time.sleep(0.119)
                pydirectinput.keyUp('d')
                pydirectinput.keyDown('w')
                time.sleep(3)
                pydirectinput.keyUp('w')
            else:
                pydirectinput.keyDown('w')
                time.sleep(0.3)
                pydirectinput.keyUp('w')
        auto_hatch = True


def format_time_ignore(seconds):
    hours = int(seconds // 3600)
    minutes = int((seconds % 3600) // 60)
    seconds = int(seconds % 60)
    return f"{hours:02}:{minutes:02}:{seconds:02}"

# 9JPL6F6YEIOW
def update_session_time_ignore():
    global total_time
    start_time = time.time()
    while True:
        elapsed_time = time.time() - start_time
        total_time = format_time_ignore(elapsed_time)
        time.sleep(1)

# Start the session time update thread
session_time_thread = threading.Thread(target=update_session_time_ignore, daemon=True)
session_time_thread.start()

# clearing the cmd
def cls():
    if os.name == 'nt':
        os.system('cls')
    else:
        os.system('clear')

def move(target_x, target_y):
    pydirectinput.moveTo(target_x + 4, target_y + 4)
    ahk.mouse_move(target_x, target_y)
    pydirectinput.click(target_x, target_y)

def nomove(x, y):
    ahk.mouse_move(x, y)

def detect_color(coords, target_color, tolerance=20):
    img = frame()
    bgr_color = img[coords[1], coords[0]]
    target_color_bgr = (target_color[2], target_color[1], target_color[0])
    diff = np.abs(np.array(bgr_color, dtype=int) - np.array(target_color_bgr, dtype=int))
    return np.all(diff <= tolerance)

def scroll(direction, amount):
    if direction == 'up':
        pyautogui.scroll(amount)
    elif direction == 'down':
        pyautogui.scroll(-amount)

def pause():
    while not running_flag:
        time.sleep(0.5)

cls()
load_assets()
bubble_prompt()
cls()
egg_prompt()
cls()
wait_prompt()
cls()
delay_prompt()
cls()
if not setup_roblox_window():
    print("Failed to setup Roblox window. Please make sure only 1 Roblox instance is running")
    input("Press Enter to continue anyway...")
print(f'Gem Genie {version} by Youngblock2k\n\nMacro running correctly\nTo start press F2, to stop press F3')
def action_loop():
    global auto_hatch, reroll_count, moved, at_egg
    while True:
        if running_flag:
            if crystals_template is None:
                return
            
            while running_flag:
                if not running_flag:
                    pause()

                screen = frame()
                card_index, score = reward(screen)

                if card_index is None:
                    if not running_flag:
                        pause()

                    move(*reroll)
                    reroll_count += 1
                    if reroll_count % 20 == 0:
                        no_orb_check()
                    time.sleep(0.3)
                    continue

                quests_found = list_quests(card_index, screen)
                print(f"[QUEST] Crystals reward at card {card_index}\n[QUEST] Card {card_index} quests {quests_found}")
                target_choice = card_choice.get(card_index)

                if target_choice:
                    move(*target_choice)
                    time.sleep(0.2)
                quest_select()

                if not running_flag:
                    pause()

                do_quests(quests_found)
                if not running_flag:
                    pause()

                while running_flag and not cleared_quests():
                    time.sleep(0.2)
                if not running_flag:
                    break

                print("Waiting for gem genie to refresh the quests")
                at_egg = False
                target_wait_id = wait_egg_target.get(wait_egg)
                if target_wait_id is not None:
                    moved = False
                    at_egg = True
                    if target_wait_id == BLOW_BUBBLES_ACTION:
                        blow_bubbles()
                    else:
                        do_quests([target_wait_id], hatching_only=True)

                if target_wait_id != BLOW_BUBBLES_ACTION:
                    wait_hatch("Quest cooldown already expired, getting a new quest")
                if not running_flag:
                    pause()

                get_quest()
        else:
            time.sleep(0.4)

# on/off switch with f2 and f3 keys
def toggle_switch(key):
    global running_flag, total_time
    if key == ON_switch:
        running_flag = not running_flag
        if running_flag:
            print(f"Script started...".ljust(60), end="\r")
        if not running_flag:
            print(f"Script paused...".ljust(60), end="\r")
    elif key == OFF_switch:
        print(f"Script stopped".ljust(60), end="\r")
        elapsed_seconds = sum(int(x) * 60 ** i for i, x in enumerate(reversed(total_time.split(":"))))
        running_flag = False
        if elapsed_seconds >= 3600:
            message = (
                f"Hello!\n\n"
                f"You have been using this macro for {total_time} hour(s).\n\n"
                f"These macros take me a long time to make, so I'd be grateful if you left a tip :)"
            )
            result = ctypes.windll.user32.MessageBoxW(
                0,
                message,
                "Thank you!",
                0x1044
            )
            if result == 6:
                import webbrowser
                webbrowser.open("https://ko-fi.com/Youngblock2k/tip")

        sys.exit()
    elif key == TIME_switch:
        print(f"Time elapsed: {total_time}")

with keyboard.Listener(on_press=toggle_switch) as listener:
    action_thread = threading.Thread(target=action_loop)
    action_thread.daemon = True
    action_thread.start()
    hatch_thread = threading.Thread(target=fast_hatch, daemon=True)
    hatch_thread.start()
    listener.join()
