/*
 * -----------------------------------------------------------------------------
 * Halfmoon JS
 * Version: 1.1.1
 * https://www.gethalfmoon.com
 * Copyright, Halfmoon UI
 * Licensed under MIT (https://www.gethalfmoon.com/license)
 * -----------------------------------------------------------------------------
 * The above notice must be included in its entirety when this file is used.
 */
Element.prototype.matches || (Element.prototype.matches = Element.prototype.msMatchesSelector || Element.prototype.webkitMatchesSelector), Element.prototype.closest || (Element.prototype.closest = function (e) {
    var t = this;
    do {
        if (t.matches(e)) return t;
        t = t.parentElement || t.parentNode
    } while (null !== t && 1 === t.nodeType);
    return null
}), "document" in self && ("classList" in document.createElement("_") && (!document.createElementNS || "classList" in document.createElementNS("http://www.w3.org/2000/svg", "g")) || function (e) {
    "use strict";
    if ("Element" in e) {
        var t = "classList",
            o = "prototype",
            a = e.Element[o],
            s = Object,
            n = String[o].trim || function () {
                return this.replace(/^\s+|\s+$/g, "")
            },
            i = Array[o].indexOf || function (e) {
                for (var t = 0, o = this.length; t < o; t++)
                    if (t in this && this[t] === e) return t;
                return -1
            },
            r = function (e, t) {
                this.name = e, this.code = DOMException[e], this.message = t
            },
            d = function (e, t) {
                if ("" === t) throw new r("SYNTAX_ERR", "The token must not be empty.");
                if (/\s/.test(t)) throw new r("INVALID_CHARACTER_ERR", "The token must not contain space characters.");
                return i.call(e, t)
            },
            l = function (e) {
                for (var t = n.call(e.getAttribute("class") || ""), o = t ? t.split(/\s+/) : [], a = 0, s = o.length; a < s; a++) this.push(o[a]);
                this._updateClassName = function () {
                    e.setAttribute("class", this.toString())
                }
            },
            c = l[o] = [],
            m = function () {
                return new l(this)
            };
        if (r[o] = Error[o], c.item = function (e) {
                return this[e] || null
            }, c.contains = function (e) {
                return ~d(this, e + "")
            }, c.add = function () {
                for (var e, t = arguments, o = 0, a = t.length, s = !1; ~d(this, e = t[o] + "") || (this.push(e), s = !0), ++o < a;);
                s && this._updateClassName()
            }, c.remove = function () {
                var e, t, o = arguments,
                    a = 0,
                    s = o.length,
                    n = !1;
                do {
                    for (t = d(this, e = o[a] + ""); ~t;) this.splice(t, 1), n = !0, t = d(this, e)
                } while (++a < s);
                n && this._updateClassName()
            }, c.toggle = function (e, t) {
                var o = this.contains(e),
                    a = o ? !0 !== t && "remove" : !1 !== t && "add";
                return a && this[a](e), !0 === t || !1 === t ? t : !o
            }, c.replace = function (e, t) {
                var o = d(e + "");
                ~o && (this.splice(o, 1, t), this._updateClassName())
            }, c.toString = function () {
                return this.join(" ")
            }, s.defineProperty) {
            var h = {
                get: m,
                enumerable: !0,
                configurable: !0
            };
            try {
                s.defineProperty(a, t, h)
            } catch (e) {
                void 0 !== e.number && -2146823252 !== e.number || (h.enumerable = !1, s.defineProperty(a, t, h))
            }
        } else s[o].__defineGetter__ && a.__defineGetter__(t, m)
    }
}(self), function () {
    "use strict";
    var e, o, t = document.createElement("_");
    t.classList.add("c1", "c2"), t.classList.contains("c2") || ((e = function (e) {
        var a = DOMTokenList.prototype[e];
        DOMTokenList.prototype[e] = function (e) {
            for (var t = arguments.length, o = 0; o < t; o++) e = arguments[o], a.call(this, e)
        }
    })("add"), e("remove")), t.classList.toggle("c3", !1), t.classList.contains("c3") && (o = DOMTokenList.prototype.toggle, DOMTokenList.prototype.toggle = function (e, t) {
        return 1 in arguments && !this.contains(e) == !t ? t : o.call(this, e)
    }), "replace" in document.createElement("_").classList || (DOMTokenList.prototype.replace = function (e, t) {
        var o = this.toString().split(" "),
            a = o.indexOf(e + "");
        ~a && (o = o.slice(a), this.remove.apply(this, o), this.add(t), this.add.apply(this, o.slice(1)))
    }), t = null
}());
var halfmoon = {
    pageWrapper: document.getElementsByClassName("page-wrapper")[0],
    stickyAlerts: document.getElementsByClassName("sticky-alerts")[0],
    darkModeOn: !1,
    createCookie: function (e, t, o) {
        var a, s = o ? ((a = new Date).setTime(a.getTime() + 24 * o * 60 * 60 * 1e3), "; expires=" + a.toGMTString()) : "";
        document.cookie = e + "=" + t + s + "; path=/"
    },
    readCookie: function (e) {
        for (var t = e + "=", o = document.cookie.split(";"), a = 0; a < o.length; a++) {
            for (var s = o[a];
                " " === s.charAt(0);) s = s.substring(1, s.length);
            if (0 === s.indexOf(t)) return s.substring(t.length, s.length)
        }
        return null
    },
    eraseCookie: function (e) {
        this.createCookie(e, "", -1)
    },
    toggleDarkMode: function () {
        document.body.classList.contains("dark-mode") ? (document.body.classList.remove("dark-mode"), this.darkModeOn = !1, this.createCookie("halfmoon_preferredMode", "light-mode", 365)) : (document.body.classList.add("dark-mode"), this.darkModeOn = !0, this.createCookie("halfmoon_preferredMode", "dark-mode", 365))
    },
    getPreferredMode: function () {
        return this.readCookie("halfmoon_preferredMode") ? this.readCookie("halfmoon_preferredMode") : "not-set"
    },
    toggleSidebar: function () {
        this.pageWrapper && (this.pageWrapper.getAttribute("data-sidebar-hidden") ? this.pageWrapper.removeAttribute("data-sidebar-hidden") : this.pageWrapper.setAttribute("data-sidebar-hidden", "hidden"))
    },
    deactivateAllDropdownToggles: function () {
        for (var e = document.querySelectorAll("[data-toggle='dropdown'].active"), t = 0; t < e.length; t++) e[t].classList.remove("active"), e[t].closest(".dropdown").classList.remove("show")
    },
    toggleModal: function (e) {
        var t = document.getElementById(e);
        t && t.classList.toggle("show")
    },
    makeId: function (e) {
        for (var t = "", o = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789", a = o.length, s = 0; s < e; s++) t += o.charAt(Math.floor(Math.random() * a));
        return t
    },
    toastAlert: function (e, t) {
        var o, a = document.getElementById(e);
        void 0 === t && (t = 5e3), a.classList.contains("show") || (a.classList.contains("alert-block") || a.classList.add("alert-block"), setTimeout(function () {
            a.classList.add("show")
        }, 250), o = t + 250, setTimeout(function () {
            a.classList.add("fade")
        }, o), setTimeout(function () {
            a.classList.remove("alert-block"), a.classList.remove("show"), a.classList.remove("fade")
        }, o + 500))
    },
    initStickyAlert: function (e) {
        var t = "content" in e ? e.content : "",
            o = "title" in e ? e.title : "",
            a = "alertType" in e ? e.alertType : "",
            s = "fillType" in e ? e.fillType : "",
            n = !("hasDismissButton" in e) || e.hasDismissButton,
            i = "timeShown" in e ? e.timeShown : 5e3,
            r = document.createElement("div");
        r.setAttribute("id", this.makeId(6)), o && (t = "<h4 class='alert-heading'>" + o + "</h4>" + t), r.classList.add("alert"), a && r.classList.add(a), s && r.classList.add(s), n && (t = "<button class='close' data-dismiss='alert' type='button' aria-label='Close'><span aria-hidden='true'>&times;</span></button>" + t), r.innerHTML = t, this.stickyAlerts.insertBefore(r, this.stickyAlerts.childNodes[0]), this.toastAlert(r.getAttribute("id"), i)
    },
    clickHandler: function (e) {},
    keydownHandler: function (e) {}
};

function halfmoonOnDOMContentLoaded() {
    halfmoon.pageWrapper || (halfmoon.pageWrapper = document.getElementsByClassName("page-wrapper")[0]), halfmoon.stickyAlerts || (halfmoon.stickyAlerts = document.getElementsByClassName("sticky-alerts")[0]), halfmoon.readCookie("halfmoon_preferredMode") ? "dark-mode" == halfmoon.readCookie("halfmoon_preferredMode") ? halfmoon.darkModeOn = !0 : halfmoon.darkModeOn = !1 : window.matchMedia && window.matchMedia("(prefers-color-scheme: dark)").matches || document.body.classList.contains("dark-mode") ? halfmoon.darkModeOn = !0 : halfmoon.darkModeOn = !1, (document.body.getAttribute("data-set-preferred-mode-onload") || document.body.getAttribute("data-set-preferred-theme-onload")) && (halfmoon.darkModeOn ? document.body.classList.contains("dark-mode") || document.body.classList.add("dark-mode") : document.body.classList.contains("dark-mode") && document.body.classList.remove("dark-mode")), document.documentElement.clientWidth <= 768 ? halfmoon.pageWrapper && (halfmoon.pageWrapper.getAttribute("data-show-sidebar-onload-sm-and-down") || halfmoon.pageWrapper.setAttribute("data-sidebar-hidden", "hidden")) : halfmoon.pageWrapper && "overlayed-all" === halfmoon.pageWrapper.getAttribute("data-sidebar-type") && halfmoon.pageWrapper.setAttribute("data-sidebar-hidden", "hidden"), document.addEventListener("click", function (e) {
        var t, o, a = e,
            s = e.target;
        s.matches("[data-toggle='dropdown']") || s.matches("[data-toggle='dropdown'] *") ? (s.matches("[data-toggle='dropdown'] *") && (s = s.closest("[data-toggle='dropdown']")), s.classList.contains("active") ? (s.classList.remove("active"), s.closest(".dropdown").classList.remove("show")) : (halfmoon.deactivateAllDropdownToggles(), s.classList.add("active"), s.closest(".dropdown").classList.add("show"))) : s.matches(".dropdown-menu *") || halfmoon.deactivateAllDropdownToggles(), (s.matches(".alert [data-dismiss='alert']") || s.matches(".alert [data-dismiss='alert'] *")) && (s.matches(".alert [data-dismiss='alert'] *") && (s = s.closest(".alert [data-dismiss='alert']")), s.parentNode.classList.add("dispose")), (s.matches("[data-toggle='modal']") || s.matches("[data-toggle='modal'] *")) && (s.matches("[data-toggle='modal'] *") && (s = s.closest("[data-toggle='modal']")), (t = document.getElementById(s.getAttribute("data-target"))) && t.classList.contains("modal") && halfmoon.toggleModal(s.getAttribute("data-target"))), (s.matches(".modal [data-dismiss='modal']") || s.matches(".modal [data-dismiss='modal'] *")) && (s.matches(".modal [data-dismiss='modal'] *") && (s = s.closest(".modal [data-dismiss='modal']")), s.closest(".modal").classList.remove("show")), s.matches(".modal-dialog") && ((o = s.closest(".modal")).getAttribute("data-overlay-dismissal-disabled") || (o.classList.contains("show") ? o.classList.remove("show") : window.location.hash = "#")), halfmoon.clickHandler(a)
    }, !1), document.addEventListener("keydown", function (e) {
        var t, o, a, s = e;
        document.querySelector("input:focus") || document.querySelector("textarea:focus") || document.querySelector("select:focus") || (e = e || window.event).ctrlKey || e.metaKey || (document.body.getAttribute("data-sidebar-shortcut-enabled") && e.shiftKey && 83 == e.which && (t = !1, window.location.hash && (o = window.location.hash.substring(1), (a = document.getElementById(o)) && a.classList.contains("modal") && (t = !0)), document.querySelector(".modal.show") && (t = !0), t || (halfmoon.toggleSidebar(), e.preventDefault())), document.body.getAttribute("data-dm-shortcut-enabled") && e.shiftKey && 68 == e.which && (halfmoon.toggleDarkMode(), e.preventDefault())), 27 === e.which && (document.querySelector("[data-toggle='dropdown'].active") ? ((a = document.querySelector("[data-toggle='dropdown'].active")).classList.remove("active"), a.closest(".dropdown").classList.remove("show"), e.preventDefault()) : (window.location.hash && (o = window.location.hash.substring(1), (a = document.getElementById(o)) && a.classList.contains("modal") && (a.getAttribute("data-esc-dismissal-disabled") || (window.location.hash = "#", e.preventDefault()))), document.querySelector(".modal.show") && ((a = document.querySelector(".modal.show")).getAttribute("data-esc-dismissal-disabled") || (a.classList.remove("show"), e.preventDefault())))), halfmoon.keydownHandler(s)
    });
    for (var e = document.querySelectorAll(".custom-file input"), t = 0; t < e.length; t++) {
        var o = e[t],
            a = document.createElement("div");
        a.classList.add("file-names");
        var s = o.getAttribute("data-default-value");
        a.innerHTML = s || "No file chosen", o.parentNode.appendChild(a), o.addEventListener("change", function (e) {
            a = e.target.parentNode.querySelector(".file-names"), 1 === e.target.files.length ? a.innerHTML = e.target.files[0].name : 1 < e.target.files.length ? a.innerHTML = e.target.files.length + " files" : a.innerHTML = "No file chosen"
        })
    }
    halfmoon.pageWrapper && halfmoon.pageWrapper.classList.add("with-transitions")
}
document.addEventListener("DOMContentLoaded", halfmoonOnDOMContentLoaded);
